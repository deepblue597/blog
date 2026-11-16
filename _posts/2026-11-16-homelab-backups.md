---
layout: post
title: "Homelab Backups I Actually Trust"
date: 2026-11-16 12:00:00 +0200
subtitle: "Database dumps, restic, an off-site box and alerts that don't lie"
background: "/assets/img/generic.jpg"
categories: [Homelab]
tags: [homelab, backups, restic, backrest, docker, self-hosting]
---

For a long time my backup strategy was hope. My homelab grew from a media stack into three machines running photos (Immich), documents (Paperless), single sign-on (Authentik), finance tracking, Home Assistant and a lot more. Every one of those apps holds data I can't re-download: family photos, scanned contracts, years of configuration. And none of it was backed up anywhere outside my house.

This post describes the backup setup I built, why each piece is there, and the mistakes I hit along the way. It's not a "copy this compose file" guide; it's about the decisions, so you can adapt them to your own lab.

**TL;DR:**

- Don't back up live database folders. Dump the databases with their **official tools** first, then back up the dumps.
- Use **restic** (through the **Backrest** web UI) to send encrypted, deduplicated snapshots **off-site**. I use a Hetzner Storage Box for about €4/month.
- Give **each host its own account** on the backup box, and turn on the box's own snapshots, so one hacked machine can't wipe everything.
- Alerts should only say "OK" when **both** the backup and the database dumps succeeded, and they should fire when **nothing** happens too.
- A backup you haven't restored is not a backup. **Test restores.**

## What actually needs a backup

The first step was the most useful one: going through every app and asking *"if this disk dies tonight, what do I lose?"* The answer splits into three groups:

| Group | Examples | Back up? |
|---|---|---|
| **Irreplaceable data** | Photos, scanned documents, databases | Yes, off-site |
| **Configuration** | App config folders, compose files, Home Assistant config | Yes, it's small and saves days of work |
| **Replaceable** | Movies, TV shows, music, caches, thumbnails, transcodes | No |

That last row matters. My media library is several terabytes; everything else is about **150 GB**. Excluding re-downloadable media turned "I need a NAS full of disks" into "I need a cheap 1 TB box".

Things I excluded on purpose:

- Media libraries and torrent downloads
- Immich thumbnails and encoded videos (Immich regenerates them from the originals)
- Jellyfin's cache and transcode folders
- Log files and the raw database folders (more on that next)

## Why not just copy the database folders?

This is the most common homelab backup mistake, and I almost made it. Postgres, MariaDB and MongoDB keep their data in files, so it's tempting to back up `./postgres-data` along with everything else.

The problem is that those files are **constantly being written** while the database runs. A backup tool copies them one by one, which can take minutes, and in that time the database keeps changing. You end up with files from different moments in time, which is a database that may not start, or worse, starts with silently corrupted data.

The fix is a **logical dump**: you ask the database itself to export a consistent snapshot (`pg_dump`, `mariadb-dump`, `mongodump`). The database guarantees the dump is consistent, even while apps keep using it. Then you back up the dump file, which is just a normal file that doesn't change.

### A tiny dump container

I looked at ready-made "db-backup" images first. The popular one had just been rewritten and re-implemented the dump logic itself, still fixing bugs. For something this important, I wanted the **official tools**, so I built a very small image:

```dockerfile
# Official PostgreSQL image (its pg_dump can dump older Postgres versions too)
# + official MariaDB / MongoDB client tools.
FROM postgres:18.6-alpine3.24
RUN apk add --no-cache mariadb-client mariadb-connector-c mongodb-tools zstd tzdata coreutils
COPY --chmod=755 dump.sh /usr/local/bin/dump.sh
USER 1000:1000
ENTRYPOINT ["/usr/local/bin/dump.sh"]
```

The script runs once a night and dumps every database on that host. The important part is how it writes files:

```sh
dump_pg() { # name host user db password
    f="$OUT/$1_$(date +%F_%H%M).dump"
    PGPASSWORD="$5" pg_dump -h "$2" -U "$3" -d "$4" -Fc -Z zstd:6 -f "$f.tmp" && mv "$f.tmp" "$f"
}
```

Each dump goes to a `.tmp` file first and is **only renamed if the dump succeeded**. A failed or interrupted dump can never leave a half-written file that looks like a good one. After all dumps, the script writes a one-line `status.txt`:

```
OK 2026-11-14T02:30:06+02:00
```

or `FAILED <date>: authentik` if something broke. That file becomes important later for the alerts.

A few more details that are worth copying:

- **`dump.sh now`** runs a single dump and exits. I use it right before risky upgrades.
- The container joins each app's Docker network, so it reaches the databases by container name. **No Docker socket**, no published ports.
- It runs with a **read-only filesystem**, as a non-root user, with all Linux capabilities dropped. A backup container sees all your passwords, so it should be able to do as little as possible.
- Dumps older than 7 days are deleted locally. The off-site copies keep the history.

## restic and Backrest

For the actual backups I use [restic](https://restic.net/), with [Backrest](https://github.com/garethgeorge/backrest) as a web UI and scheduler on top.

Why restic:

- **Client-side encryption.** Data is encrypted before it leaves the machine, so the storage provider only ever sees encrypted blobs.
- **Deduplication.** Every snapshot looks like a full backup, but only changed chunks are uploaded. My nightly runs take **under 30 seconds** after the first big upload.
- **Compression.** Configs and dumps shrink a lot. My first server snapshot compressed about 2×.

One consequence: **don't zip or encrypt files yourself before backing them up.** A zip changes completely when one file inside it changes, which breaks deduplication, and restic already encrypts and compresses.

Why Backrest on top: restic alone works fine from a cron job, but Backrest gives me schedules, retention, a list of snapshots, a "restore this folder" button, and **hooks**, which turned out to be the most useful part.

### Run it with as few permissions as possible

Backrest needs to *read* files owned by many different users (each app writes its data as a different user). Instead of giving it full root, I drop every capability except the one that allows reading any file:

```yaml
backrest:
  image: ghcr.io/garethgeorge/backrest:v1.14.1
  user: "0:0"
  cap_drop: [ALL]
  cap_add: [DAC_READ_SEARCH]   # read any file, nothing else
  security_opt: [no-new-privileges:true]
  volumes:
    - /path/to/app-configs:/sources/configs:ro
    - /path/to/db-dumps:/sources/db-dumps:ro
    - /path/to/restore:/restore            # the only writable data path
```

All sources are mounted **read-only**. The only writable folder is a dedicated restore target. Even if Backrest had a bug, it couldn't damage the data it's backing up.

## Off-site: a Hetzner Storage Box

The classic **3-2-1 rule** says: 3 copies, on 2 types of storage, 1 of them off-site. Having the live data and one off-site copy covers the scenario I care about most: fire, theft, a dead disk, or ransomware in the house.

I chose a **Hetzner Storage Box** (1 TB, about €4/month with VAT, unlimited traffic, in the EU). It's not a server, so there's no operating system for me to maintain; it just speaks SFTP, which restic supports out of the box.

Things I learned setting it up:

- **SFTP runs on port 23**, not 22.
- **One sub-account per host.** Each machine gets its own sub-account, locked to its own folder and an SSH key. If one machine is compromised, it can't see or delete the backups of the others.
- Sub-accounts **need "External reachability" turned on**. With it off, SSH answers "Permission denied" without even listing any login methods, which took me a while to understand.
- Sub-accounts have no SSH-key field in the web panel; you add the key to `.ssh/authorized_keys` inside the sub-account's folder.
- **Pin the host key** (`StrictHostKeyChecking=yes` with a fixed `known_hosts` file) instead of trusting whatever answers. Backrest's own UI checks `/root/.ssh/known_hosts`, so I mount the same file there too.
- **Turn on the box's automatic snapshots.** This is the ransomware protection: if an attacker gets into a server and deletes its restic repository, the Storage Box still has read-only snapshots from the previous days that the server can't touch. I keep 10 daily snapshots.

The restic repository in Backrest then looks like this:

```
sftp:<sub-account>@<sub-account>.your-storagebox.de:repo
-o "sftp.args=-i /ssh/storagebox_key -p 23 -oUserKnownHostsFile=/ssh/known_hosts -oStrictHostKeyChecking=yes -oBatchMode=yes"
```

**The restic password is the only key to your backups.** If you lose it, the backups are unreadable forever, even for you. Mine is in my password manager *and* written down outside the homelab. A password manager that's backed up only by the homelab doesn't count.

## The nightly schedule

Each host runs the same pattern, staggered so they don't all hit the box at once:

| Time | Server | Photo/docs host | Raspberry Pi |
|---|---|---|---|
| 02:30 / 02:45 | DB dumps | DB dumps | — |
| 03:00 / 03:15 / 03:30 | Backup | Backup | Backup |
| Sunday 04:00–05:00 | Prune old snapshots | Prune | Prune |
| 1st of the month | `restic check` | `restic check` | `restic check` |

Retention is **7 daily, 4 weekly, 6 monthly** snapshots. Thanks to deduplication, that's 17 restore points for roughly the size of one full copy plus changes.

The Pi doesn't need a dump container: Home Assistant makes its own daily backups, and the Pi's other services (Pi-hole, OpenMediaVault) keep their config in `/etc`, which is backed up as files.

## Alerts that don't lie

A backup that silently stopped working three months ago is worse than no backup, because you *think* you're safe. So the alerts had two requirements:

1. Say "OK" only when **everything** worked: the database dumps *and* the upload.
2. Alert when **nothing happens**, e.g. the machine is off or the container crashed. A system that only sends "failed" messages stays silent in exactly that case.

I already had **Uptime Kuma** sending alerts to Telegram, and it has a perfect feature for this: **push monitors**. You give the monitor a heartbeat interval, and if no "up" message arrives in time, it alerts. I set it to **26 hours**: a daily job plus some slack.

Backrest's hooks then push to Kuma. On a successful snapshot, the hook first checks that today's dumps are OK:

```sh
S="$(cat /sources/db-dumps/status.txt 2>/dev/null)"
case "$S" in
  "OK $(date +%F)"*) curl -fsS "$KUMA_PUSH_URL?status=up&msg=backup+OK,+DB+dumps+OK" ;;
  *)                 curl -fsS "$KUMA_PUSH_URL?status=down&msg=backup+OK,+but+DB+dumps+failed" ;;
esac
```

Plus a few more hooks:

- **Before the backup starts:** if the dumps aren't fresh, the snapshot is cancelled and the monitor goes down.
- **On any error, or if a prune or check fails:** push `down`.

So my phone gets a message if a dump fails, the upload fails, the repository check fails, or **nothing reports at all for 26 hours**. On a normal night, I hear nothing.

One small gotcha: keep hook commands on short lines. A long `curl` line that got split while copy-pasting broke silently in one of my hooks, and `sh -n` (the syntax check) still passed.

## Restore tests: the part that matters

Everything above is just a theory until you restore something. My tests:

- **Authentik** (my single sign-on, the most critical database): I restored last night's dump from the Storage Box, checked its sha256 against the original, and loaded it into a **throw-away Postgres container with no network** (`--network none`). Then I compared it with the live system: same number of users, apps, groups, login flows and 2FA devices.
- **Photos**: restored a random photo plus the Immich database dump, compared the photo's checksum (identical) and checked the dump contained all tables.
- **Raspberry Pi**: restored Pi-hole and OpenMediaVault config files and the Home Assistant config. All checksums matched, and the Home Assistant backup archive opened fine.

Two things I only found out by testing:

- The first restore attempt failed with a **repository lock**. The first night's prune and check were still running. Restic locks the repository during maintenance; just wait for it to finish.
- Restored files **lose their original owner**, because Backrest deliberately has no permission to change file ownership. The content is fine, but if you restore something into `/etc`, you have to fix the owner and permissions by hand.

My rule now: **a small restore test every month**, and a real one before any big upgrade.

## Keeping it all in Git

The backup stacks themselves live in a private Git repository (one folder per host) and are deployed with [Komodo](https://komo.do). That means:

- The setup is documented and reproducible. If a host dies, I redeploy its backup stack from Git and restore.
- The passwords aren't in Git. They're stored as **secret variables** in Komodo and only injected at deploy time.
- One gotcha with locally built images like the dump container: add `pull_policy: build`. Otherwise Komodo tries to pull `local/db-dump` from a registry on every deploy and fails.

Backrest's own configuration (repositories, plans, hooks, the restic password) lives in its config folder on the host, *not* in Git, because it contains secrets.

## What it costs and what's left

- **Money:** about €4/month for the Storage Box. Everything else is open source.
- **Resources:** the dump container uses about 50 MB of RAM and runs for seconds. Backrest idles at about 100 MB.
- **Time:** about two evenings to build and test, plus a few minutes a month for restore tests.

It's not perfect. My media library still has no redundancy at all (by choice, since it's replaceable, but re-downloading terabytes would hurt). And the restore tests only work if I actually do them.

But for the first time, I know that if a disk dies tonight, I lose at most one day of photos and documents, and I'll get a message on my phone telling me so.

If you run a homelab without off-site backups: start with the one database you'd miss most, dump it properly, send it somewhere outside your house, and **restore it once**. Everything else can come later.
