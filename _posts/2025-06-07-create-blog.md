---
layout: post
title: "Create a simple blog!"
date: 2025-06-07 00:30:08 +0300
subtitle: "A guide to a simple blog page."
background: "/assets/img/blog-bg.jpg"
author: jason
---

For a lot of tech enthusiasts, creating their first public page is a big achievement. A sense of accomplishment that something is now
public and can be seen by anyone. You can share it with your friends and have some fun (even brag a bit about it). So as i developed today this blog
i think it would be a great opportunity to share how i started this blog.

First of all I didn't want or need anything fancy. A simple page that i would be able to write about my hobbies, my projects and generally my interests.
Furthermore I didn't want to pay for anything or work a lot on it. I frist thought on using my raspberry pi as a server for my blog. It sounded like a good idea
to learn a bit more about hosting websites. Truth be told, wheni started reading about port forwarding, some PTSD started kicking in from my attempt to forward a port from my vpn in order to use it for a qbittorent project (more on that later). So I asked ChatGPT what would be an easier solution, and that's when it suggested using Jekyll with GitHub pages. I had some experience with GitHub pages, but I didn't know that I could host one page per project, which sounded pretty awesome and easy for me. I started checking on [Jekyll](https://jekyllrb.com/) and it seemed pretty straight forward. I also searched for some templates and voila! it was time to start working on my blog. So, let's get first things first

## Step 1: Prerequisites

Based on the [Jekyll documentation](https://jekyllrb.com/docs/), You will need 3 things

- Ruby version 2.7.0 or higher
- RubyGems
- GCC and Make

For Ubuntu you can check [Jekyll documentation](https://jekyllrb.com/docs/installation/ubuntu/). You need to run

{% highlight bash %}
sudo apt-get install ruby-full build-essential zlib1g-dev
{% endhighlight %}

Then for RubyGems
{% highlight bash %}
echo '# Install Ruby Gems to ~/gems' >> ~/.bashrc
echo 'export GEM_HOME="$HOME/gems"' >> ~/.bashrc
echo 'export PATH="$HOME/gems/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc
{% endhighlight %}

and finally
{% highlight bash %}

gem install jekyll bundler
{% endhighlight %}

**Note**: For me the final command didn't work (the eror was `It is likely that you need to grant write permissions for that path.`). You can try to fix permissions inside your project's folder (will talk about how to create one) by using

```
sudo chown -R $USER:$USER .
```

and then `bundle install`.

But if this doesn't work you could do
`sudo bundle install` but it is not recommended.

## Step 2: Create your file's project

This is a straight forward step. To make a jekyll project you run

{% highlight bash %}
jekyll new <YOUR_BLOG_NAME>
cd <YOUR_BLOG_NAME>
bundle exec jekyll serve
{% endhighlight %}

This will run your site on `http://localhost:4000`

## Step 3: Themes!

Without some sazzle and dazzle, the blog seems pretty boring. Let's change that! You can check different themes on [jekyllthemes.io](https://jekyllthemes.io/). Some are free some are paid. I chose [this clean blog theme](https://jekyllthemes.io/theme/startbootstrap-clean-blog-jekyll). You can find the installation guide [on the theme's page](https://github.com/StartBootstrap/startbootstrap-clean-blog-jekyll) but I name the steps. So, in order to apply it to your jekyll blog you need to:

1. Replace the current theme in your Gemfile with gem "jekyll-theme-clean-blog". Go to `Gemfile` and fing the 'gem "minima", "~> 2.5" ' attribute. Change this.
2. Install the theme (run the command inside your site directory): `bundle install`
3. Replace the current theme in your \_config.yml file with theme: jekyll-theme-clean-blog. `theme: jekyll-theme-clean-blog`
4. Build your site: `bundle exec jekyll serve`
