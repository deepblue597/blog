---
layout: post
title: "Thesis tools 101"
date: 2025-06-27 18:34:08 +0300
subtitle: "Tools that will help you work on your thesis."
background: "/assets/img/thesis.jpg"
---

Hello my fellow students (and not). This time i decided to write about something that really struggles me for 9 months now. Thesis: A whole project that a master student needs to do in order to get his/her degree. It includes, a project (either a research or a more technical one), the thesis itself which is a 70-ish page document in which you write what you did, what did other people do up until now, theory in which you explain core concepts that your thesis is based upon, your implementations (whether that is a theoretical development or a practical explanation on what you developed), results and future development, and maybe a paper which is a brief explanation of your work that you can present ona forum.

In this article, I thought of naming a few tools that have helped me thus far with the development of my project and the writing of my thesis.

My thesis is a more technical one. I am developing a DSL for machine learning in live data. I am naming it beaver!!! I will write about it on another blog post because i am really proud of my work and i want to help other people working with machine learning algorithms. So, these tools might not help everyone, it is more tailored towards software engineering students, but I hope some of them can really be helpful to every students battling with his/her thesis. So without further ado, here are my thesis tools!

## Notion

First on our list is [Notion](https://www.notion.so/). Notion is a cloud Note taking app, with a lot of layouts and multiple features. You write on Markdown and you can create pages, bullets, add embedded frames and many more. You can also collaborate with other people and publish your page! There is a free plan as well as paid plans. Me personally, the free plan fully covers me so i don't need to pay for any features. I am mainly using it for keeping track of my sources, my progress and showing my questions to my teachers for further explanations. Furthermore, i keep notes (shocking) from videos, tutorials and documentation pages i study in order to solve any problems i have encountered thus far. I also use for other stuff, like notes for my courses, some supermarket chores and i have also used it as a collaborative tool when i was working at SpaceDot. It can really simplify your note taking tasks so i highly recommend it. There are also some other tools similar to Notion like [Obsidian](https://obsidian.md/) which might suit you more.

## Git(hub)

Coming up next on No.2 is Git and specifically [GitHub](https://github.com/). Git is a software, more specifically a version control software that lets you track changes of your files over time. GitHub is a platform in which you can upload your code and keep track of the changes you do. GitHub is a platform where you can find other projects, download them, report issues and connect with other developers. But for our case is tool that helps us developing our project. How many times have you created a final_final_final file that in the end it wasn't the final one? How many times have you forgotten to save your file or even worse, lost it? How many times have you wanted to use another computer and you couldn't because you didn't have your project? Well fear not my fellow engineer, these problems are no more. With git you can keep track of your development, create new branches in which you can work on a new project without interfearing with the main development branch (thus maybe breaking it) and even more, you can collaborate with other people on different features without creating problems one another. If you don't want to use GitHub there is also [GitLab](https://about.gitlab.com/). You can also publish your work and serve it through GitHub. This whole blog is served on GitHub! And most importantly, you can showcase your work, which is really important when you start searching for a job. I firmly believe that this tool is essential for any software engineer and generally anyone working with developing code.

## VsCode

[VsCode](https://code.visualstudio.com/) (Visual Studio Code) is a text editor. You can write your code there. I don't think there is another Text editor more prevalent and more dominant than this. Lots of tools, lots of extension in an easy to use GUI. I don't have many more to say, other than I am writing on VsCode this blog.

## Docker

I have already talked about docker on [a previous post](https://deepblue597.github.io/blog/2025/06/14/media-stack.html). It is a way to use apps with all the necessary dependencies without being afraid of not working on another pc. I have used in on multiple occasions especially on my self hosting apps due the ability to turn down and up whichever app i want and update them without any issues. Furthermore a lot of apps will occupy a port, and most of the times they try to occupy the same one. With docker you can specify which port the container to use, where to save the data and many more configuration options. On my thesis case i used it to create a kafka cluster (more on that on the next post about my thesis). I think it is really helpful to know how docker works and how configure a few apps. You don't need to be an expert, just to understand how youc an use it. My next endeavour will be understanding kubernetes

## Youtube

This seems really obvious but, on youtube you need to know HOW to search something not only what to. Because there a lot of videos from multiple sources that might not be what you search for, or even worse, misinform you. Especially now that you can see the dislike counter it is really easy to search for an explanation on a certain subject, and due to promotion reasons, a video pops up that is inaccurate and set you back, or even worse, make you understand something wrong. What i recommend is checking the youtube channel is it has any reputation and even more, check on the comments on the videos. This will give you a better understanding if you should watch it or not

## ChatGPT

Again, an obvious addition but again, you need to be really careful with how you use ChatGPT. It is a tool, and a tool is only good if you know how to properly use it. In this case, you need to always check what ChatGPT says and verify it with your own research. Basic questions and general knowledge will probably be correct. But ask it something really specific on a niche field, and you are cooked. Furthermore, ChatGPT is not really good at reading fills you feed it. There have been multiple times that I feed him a paper, and the outcome is something totally irrelevant.

I suggest using different chats for different subjects and try to be as specific with your question as possible. If something feels that is not correct, ask him again and pinpoint your doubts about the certain part that you are not sure. If the outcome is something different, i would highly suggest checking on the internet or ask him about his resources.

When we are talking about coding, again, Chat can be really good with some general code snippets with some basic aspects, but ask him about something hard or nuance, and you walking uncharted territory. Remember chat can only answer you about question he was learned to answer from the gathering of data across the internet. So basic general question that everybody does --> really good at answering. Something really specific in a certain field and you need to take everything is says with a pinch of salt.

## NotebookLM

Now, this is a LLM created for thesis purposes. NotebookLM is using the info you provide him to answer question. It can't answer general questions that your sources don't provide info for. It will also give you the exact place where it supports its answer. You can create a recording in which Notebook will have a small discussion using 2 voices to help you understand what the sources say, as well as notes and a study guide. I really use when i want to understand the papers that i am reading and chat is not a reliable source in such cases. One caveat about NotebookLM is that, it doesnt save your discussion, only what you explicity say to it to save it as a note. So keep that in mind if you want to save something to remember it for later

## Overleaf

Overleaf is a cloud editor for LateX. Is really useful when you write your thesis because most of the thesis and papers are written in LateX. You can specify the layout, the font, the design and how images and charts will be incorporated in your article. Furthermore you can collaborate with other people.

## Paperless-ngx

No we are getting in some niche fields for the truly passioante about finding new apps to work with. Paperless-ngx is a self hosting app in which you can save doccuments. But jason you might say, what does this have to do with my thesis? Well my petite croissant, if you want to save the papers that you read and be able to access them from different devices, then paperless is the tool for you. Long gone the days with multiple sheets of paper, with binders and what not to keep your documents. Paperless help you organize this mess and throw away all this unnecessary mess. It can also help you with other aspects of your life such as: agreements, bank notes, bills etc.

## Karakeep

## SlidesGo
