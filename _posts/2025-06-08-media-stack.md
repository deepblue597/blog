---
layout: post
title: "Self hosted media stack"
date: 2025-06-08 18:34:08 +0300
subtitle: "Start hosting your own netflix."
background: "/assets/img/media-stack.jpg"
---

During the early 10s netflix was the king of media ententertainment. It was the first platform that offered a wide range of movies and series for a small monthly fee. It was revolutionary and it changed the way we consume media. But as time passed, netflix started to lose its charm. The subscription fee increased rapidly, the content wasn't as interesting as before and more and more companies started entering the on the game. Disney, HBO, ESPN, all started having their own subscripiton plans and hosted their content on their own platforms. Furtermore, password sharing crackdowns increased and people couldn't divide the cost of the susbscriptions. That's when, people started looking on alterinative options for watching their favourite tv show or movie, and self hosting started reappearing on the horizon. In this blog, we will talk about self hosting and how you could run your own self hosting media stack. Let's talk about it more in depth!

## Disclaimer

I don't condone or encourage downloading, sharing, seeding, or peering of copyrighted material.
Such activities are illegal under international laws.
This article is intended for educational purposes only.

## What is self hosting

Self hosting means hosting your apps on your own server. It is great if you want to keep your data private and have the full control of them. In order to host your own apps all you need is a pc/laptop (preferably with Ubuntu installed). Your old laptop or pc could be a great fit for such case. Why wouldn't you use your current pc? Well, you could but the pc needs to be always on in order to access your apps. Furthermore it will use your pc's resources and storage in order to function, which might not be bad if you have 1 or 2 apps running, but when we are talking about multiple apps this may cause an issue. Now that we have mentioned a few things about self hosting, let's talk about today's project.

## Media stack

The media stack we will be using consists of

- vpn (using gluetun)
- qbittorent
- prowlarr
- sonarr
- radarr
- jellyfin
- jellyseer

The project we will be following is [the media stack by navilg](https://github.com/navilg/media-stack)

## Docker

Docker is a platform as a service products that use OS-level virtualization to deliver software in packages called containers. In simpler words, you can define an app inside a docker, with its variables, os needs and versions, "containerize" and distribute it to any pc you want, without fearing that it won't work. What it does is defining the exact parameters that are needed in order for the app to work, so that if you run the app on another pc with different parameters, apps, or versions of apps, the docker app will use the parameters given by the container and run it without any issues. This is really important for app development. Engineers are no longer afraid of 'but it worked on my pc' cases that are a result of a different package, version or variable set between different pcs.

## Vpn

VPN (Virtual Private Network) is a way for anyone to acess the internet without using his/her real ip. You are connecting to another pc/server and it mkaes the requests you ask for example visiting YouTube or Spotify or any other website. The apps will only know the server's ip, not yours. This means that they can't identify you and connect you with the request you made. VPN is not a company nor an app, it's a technology that create a secure connection with a server. This means that you don't need to pay a company to use VPN, you just need to pcs to create a VPN connection. But then. why do we pay companies for using a VPN. Well, for providing us with the access to their servers, for ensuring a stable, fast and secure connection and for not storing our data (no logs policy). Remember, using a friend's pc for a vpn connection, means that your friend will know that you connected to his/her pc and the ip that the apps will see for the requests will be your friends. In order to be secure on the internet, you don't want to endanger your friend. That is why we use VPN companies. The are multiple companies and some of them have free plans, but i would recommend paying something and searching for notable companies in order to have your mind at peace. Some of the most notable apps are NordVPN, ProtonVPN, Mullvad. You can check [PC Mag's Best VPN Services for 2025](https://www.pcmag.com/picks/the-best-vpn-services?test_uuid=02LlF0iWKsilxYTJVF8uH5y&test_variant=A) to find out more info about each option
