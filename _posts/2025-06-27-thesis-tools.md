---
layout: post
title: "Thesis tools 101"
date: 2025-06-27 18:34:08 +0300
subtitle: "The Tools That Helped Me Survive My Thesis"
background: "/assets/img/thesis.jpg"
---

Hello my fellow students (and not). This time I decided to write about something that has been really challenging for me for the past 9 months: my thesis.

For those unfamiliar, a thesis is a major project that a master’s student (or in some cases, a bachelor’s student) needs to complete in order to get their degree. It includes:

- A project (either research-based or more technical)

- The thesis document itself: a ~70-page text where you explain what you did, what others have done up to now, the theory behind it, your implementation, results, and possible future work

- And sometimes even a paper: a brief summary of your work that can be submitted to a conference or journal.

In this article, I thought I’d share some tools that have helped me so far with both the development of my project and the writing of my thesis.

My thesis is more on the technical side. I am developing a DSL (Domain Specific Language) for machine learning on live data streams. I am naming it Beaver!!! 🦫 I will write about it in another blog post because I am really proud of my work, and I want to help other people working with machine learning algorithms.

These tools might not help everyone, as they are more tailored towards software engineering and data science students, but I hope some of them can be helpful to any student battling with their thesis.

So, without further ado, here are my thesis tools!

## Notion

First on our list is [Notion](https://www.notion.so/). Notion is a cloud-based note-taking and knowledge management app with a lot of layouts and features. You can write using Markdown, create nested pages, bullet lists, embedded frames, databases, kanban boards, and much more. You can also collaborate with other people and publish your pages publicly.

There is a free plan available, as well as paid options, but personally, the free plan fully covers my needs. I mainly use Notion to track my sources and references, organize my progress by keeping tabs on which chapter I’m writing and what’s still pending, document questions for my professors and supervisors, and take detailed notes from videos, tutorials, and documentation pages that help me solve problems I encounter during my research.

Beyond my thesis, I also use Notion for managing my university courses, keeping supermarket lists, and collaborating on projects. In fact, I relied on it extensively when I worked at SpaceDot, where it helped keep our team organized and on the same page.

It can truly simplify your note-taking and organization tasks, so I highly recommend it. Some alternatives to Notion are [Obsidian](https://obsidian.md/) and [Logseq](https://logseq.com/) if you prefer local storage and graph-based notes.

Below is a glimpse of my thesis Notion page. I couldn’t fit all the subpages, but you can see how I organize each section of my thesis:

<div style="text-align: center; margin: 20px 0;"> <img src="{{ site.baseurl }}/assets/img/notion.png" alt="Notion" width="400"> </div>

## Git(hub)

Coming up next on No.2 is Git and specifically [GitHub](https://github.com/).Git is a version control software that lets you track changes in your files over time. GitHub is an online platform where you can upload your code repositories and keep track of all your changes, collaborate with others, and showcase your work.

GitHub is not just a place to store your code — it’s also a huge community where you can discover other projects, download and contribute to open-source code, report issues, and connect with fellow developers. For our purposes, though, it mainly serves as a tool to help us develop our projects safely and efficiently.

How many times have you created a file named final_final_final only to realize it still wasn’t the final version? Or forgotten to save your work, or even worse, lost it completely? Maybe you wanted to continue working on another computer but didn’t have your project with you. Fear not, my fellow engineer, because these problems are a thing of the past. With Git, you can keep track of your development history, create branches to work on new features without affecting the main project (and potentially breaking it), and collaborate smoothly with others on the same project without causing conflicts.

If you don’t want to use GitHub, there is also [GitLab](https://about.gitlab.com/) as alternative.

You can even publish your work and serve it through GitHub Pages. This entire blog, for example, is served on GitHub! Most importantly, GitHub helps you showcase your projects and skills to future employers, which is crucial when you start job hunting.

I firmly believe that Git (and GitHub) is an essential tool for any software engineer, and generally for anyone working with code.

Below is part of my [GitHub thesis repo](https://github.com/deepblue597/thesis):

<div style="text-align: center; margin: 20px 0;">
<img src="{{ site.baseurl }}/assets/img/beaver.png" alt="Beaver" width="400">
</div>

## VsCode

[VsCode](https://code.visualstudio.com/) (Visual Studio Code) is a text editor. You can write your code there. Well… not just any text editor. You can write your code there, debug it, test it, and even deploy – all from one place. I don’t think there is another text editor more prevalent and dominant than this right now. It supports almost every programming language and framework you can think of, and its marketplace has thousands of extensions to make your life easier.

It has Git integration, an integrated terminal, debugging tools, and a Markdown preview (I am actually writing this very blog post on VSCode!). Its GUI is easy to use and fully customizable, so you can set it up exactly how you like to work.

I don’t have much more to say, other than: if you’re coding, use VSCode.

## Docker

I have already talked about docker on [a previous post](https://deepblue597.github.io/blog/2025/06/14/media-stack.html). In short, Docker is a way to use apps with all their necessary dependencies, without worrying whether they will work on another PC.

I have used it on multiple occasions, especially for my self-hosting apps, because it gives me the ability to turn any app up or down whenever I want, and update them without any issues. Furthermore, a lot of apps try to occupy the same ports, which creates conflicts. With Docker, you can easily specify which port each container will use, where to save its data, and many more configuration options.

For my thesis, I used Docker to create a Kafka cluster (more on that in my next post about my thesis). I think it is really helpful to know how Docker works and how to configure a few apps with it. You don’t need to be an expert – just understanding how to use it for your workflow will make your life much easier.

My next endeavour will be understanding Kubernetes, but that’s a story for another day.

## Youtube

This seems really obvious but, on [Youtube](https://www.youtube.com/) is a tool you need to know how to use, not just what to search for. There are countless videos from multiple sources, and many of them might not be what you’re actually looking for – or even worse, they might misinform you. Especially now that you can’t always see the dislike counter easily, it’s harder to filter out low-quality content. You might search for an explanation on a certain subject, and due to promotion reasons, a video pops up that is inaccurate, sets you back, or makes you understand something wrong.

What I recommend is this: check if the YouTube channel has any reputation, see if it has consistent quality content, and most importantly, read the comments. Comments often reveal if the video is worth your time or if it’s misleading.

## ChatGPT

Again, an obvious addition but again, you need to be really careful with how you use [ChatGPT](https://chatgpt.com/). It is a tool, and a tool is only good if you know how to properly use it.

You always need to check what ChatGPT says and verify it with your own research. For basic questions and general knowledge, it will probably be correct. But if you ask something really specific in a niche field, you might be in trouble. Furthermore, ChatGPT is not really good at reading files you feed it. There have been multiple times where I gave it a paper, and the outcome was something totally irrelevant.

I suggest using different chats for different subjects and trying to be as specific with your question as possible. If something feels off, ask again and pinpoint your doubts about the specific part you are unsure about. If the outcome is different the second time, I highly recommend checking on the internet or asking it directly about its sources.

When it comes to coding, ChatGPT can be really good with general code snippets and basic concepts. But if you ask about something hard or nuanced, you are walking into uncharted territory. Remember: ChatGPT can only answer questions it has been trained to answer from data gathered across the internet. So for basic, general questions that everyone asks – it’s really good. But for something highly specific in a certain field, take everything it says with a pinch of salt.

## NotebookLM

Now, this is a LLM created for thesis purposes. [NotebookLM](https://notebooklm.google.com/) uses the info you provide to answer your questions. It can’t answer general questions that your sources don’t cover. The good thing is that it will also give you the exact place where it supports its answer.

You can create a recording in which NotebookLM has a small discussion using two voices to help you understand what your sources say, as well as generate notes and a study guide. I really use it when I want to understand the papers I’m reading, especially when ChatGPT is not a reliable source in such cases.

One caveat about NotebookLM is that it doesn’t save your discussions, only what you explicitly save as a note. So keep that in mind if you want to revisit something later.

## Perplexity

Rounding up the AI tools, I am referencing an AI engine. [Perplexity](https://www.perplexity.ai/) is an AI search engine, meaning that it not only provides you with an answer to your question but also shows you the sources it used to produce that answer. You can use it like a normal search engine as well. I think it’s a nice tool that complements the previous two.

## Overleaf

[Overleaf](https://www.overleaf.com/) is a cloud editor for LaTeX. It’s really useful when writing your thesis because most theses and papers are written in LaTeX. You can specify the layout, fonts, design, and how images and charts are incorporated in your document. Furthermore, you can collaborate with other people in real-time, which is great if your supervisor wants to edit or comment directly on your thesis.

## Paperless-ngx

No we are getting in some niche fields for the truly passionate about finding new apps to work with. [Paperless-ngx](https://docs.paperless-ngx.com/) is a self-hosting app where you can save and organize your documents.

But Jason, you might say, what does this have to do with my thesis? Well, my petite croissant, if you want to save the papers you read and access them from different devices, then Paperless is the tool for you. Long gone are the days of multiple sheets of paper, binders, and folders to keep track of your documents.

Paperless helps you organize this mess and throw away all that unnecessary clutter. It can also help with other aspects of your life, such as agreements, bank notes, bills, and any other documents you want to keep safely archived and easily searchable.

<div style="text-align: center; margin: 20px 0;">
<img src="{{ site.baseurl }}/assets/img/documents-smallcards-dark.png" alt="Paperless ngx" width="400">
</div>

## Karakeep

This is an app that I really enjoy using since it helps me organize my bookmarks. [Karakeep](https://karakeep.app/) is a self-hosting app that manages your bookmarks with the help of AI.

You save a site to the app, and then you can search for it either by its name or by the content of the page. Furthermore, with the help of ChatGPT, it automatically adds tags to your bookmarks. So even if you don’t remember the name or the content of the site you want to find, but you know it was about machine learning, you can just type “machine learning” in the search bar, and it will show all the bookmarks related to it.

I personally find this really convenient since I tend to bookmark lots of pages. Most of the time I’m too bored to create appropriate folders, or the folders I have are stuffed with so many sites that it’s really hard to find what I want. With Karakeep, I can just type what I’m looking for and retrieve it instantly.

In addition, you can also take a snapshot of the site the moment you save it. This means that if the page goes down later or you need the exact version of that page as it was when you saved it, you can always find and use it via the Karakeep app.

<div style="text-align: center; margin: 20px 0;">
<img src="{{ site.baseurl }}/assets/img/karakeep.webp" alt="karakeep" width="400">
</div>

## File Browser quantum

his is another somewhat niche app, but I’ve found it incredibly useful when I’m away from home. I have a PC where I do most of my work, and I use my laptop when I’m outside. Since my laptop doesn’t have much storage space, I save a lot of my files—especially books for my thesis—on my PC.

This creates a problem: I can only access those files when I’m at home. To fix this, I’d normally have to keep copies on my laptop or upload them to a cloud service, which can be a hassle.

That’s where [FileBrowser Quantum](https://github.com/kenrmayfield/filebrowserquantum) comes in. Instead of storing multiple copies and filling up my laptop with PDFs, I can remotely access my PC’s files through this self-hosted file browser app. I just log in, and I can download, upload, or simply browse the files I have on my PC.

I really appreciate this option, especially when I’m far away from home and don’t want to wait until I get back to access important files.

<div style="text-align: center; margin: 20px 0;">
<img src="{{ site.baseurl }}/assets/img/filebrowser.jpeg" alt="filebrowser" width="400">
</div>

## Tailscale

Apps like Karakeep, Paperless-ngx, and FileBrowser Quantum often run on another PC or a server (like a Raspberry Pi), and you might want to access them remotely. You could set up a WireGuard tunnel yourself or configure a reverse proxy to communicate with your server, but the easiest and most user-friendly option I found is [Tailscale](https://tailscale.com/).

Tailscale is an app that creates a secure connection between your devices using WireGuard technology. While I highly recommend setting up a WireGuard tunnel manually at least once to understand how it works, Tailscale offers a plug-and-play experience that makes it incredibly simple to use.

If you’re interested in self-hosting or just want a hassle-free way to connect your devices securely, Tailscale is definitely a tool worth exploring.

<div style="text-align: center; margin: 20px 0;">
<img src="{{ site.baseurl }}/assets/img/tailscale.svg" alt="tailscale" width="300">
</div>

## SlidesGo

Last but not least, I want to share a website full of presentation layouts. When I present my progress to my tutor, I don’t want to waste time designing a nice layout or end up with a blank, boring presentation showing only my progress.That’s where [SlidesGo](https://slidesgo.com/) comes in. It offers tons of free presentation templates that look professional and help showcase your work effectively. I find it really useful and love their designs.

## Conclusion

These are most of the tools I’m using to complete my thesis. Each one plays an important role in helping me develop, organize, and write my project, and I genuinely enjoy using them all. I hope this overview helps you discover useful tools for your own work. If you have a favorite tool you’d like to recommend, write me—I’d love to check it out!

See you in the next blog post! 🤓
