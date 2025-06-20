---
layout: post
title: "Create a simple blog!"
date: 2025-06-07 00:30:08 +0300
subtitle: "A guide to a simple blog page."
background: "/assets/img/blog-bg.jpg"
---

For a lot of tech enthusiasts, creating their first public page is a big achievement. A sense of accomplishment that something is now
public and can be seen by anyone. You can share it with your friends and have some fun (even brag a bit about it). So as i developed today this blog
i think it would be a great opportunity to share how i started this blog. 🔥

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

Now you need to check if there are certain files on your root folder.

- `index.html`
- `about.html`
- `contact.html`
- `posts/index.html`

I would suggest checking the documentation's [demo page](https://github.com/StartBootstrap/startbootstrap-clean-blog-jekyll) on how to populate them. For example on `posts/index.html` you can put something like

{% highlight html %}

    {% for post in site.posts %}

<article class="post-preview">
  <a href="{{ post.url | prepend: site.baseurl | replace: '//', '/' }}">
    <h2 class="post-title">{{ post.title }}</h2>
    {% if post.subtitle %}
    <h3 class="post-subtitle">{{ post.subtitle }}</h3>
    {% else %}
    <h3 class="post-subtitle">
      {{ post.excerpt | strip_html | truncatewords: 15 }}
    </h3>
    {% endif %}
  </a>
  <p class="post-meta">
    Posted by {% if post.author %} {{ post.author }} {% else %} {{ site.author
    }} {% endif %} on {{ post.date | date: '%B %d, %Y' }} &middot; {% include
    read_time.html content=post.content %}
  </p>
</article>

<hr />

{% endfor %}
{% endhighlight %}

**Note** Jekyll supports Liquid template tags so to use the same template for every post you can wrap the previous code around {% raw %}{% for post in site.posts %} {% endfor %} {% endraw %}

You also need to configure your `baseurl` `url` `email` `author` `title` and `description` on your `_config.yml` file. When you do so on your terminal press
`Ctr+C` and then `bundle exec jekyll serve`

**Note** I couldn't make the contact page work so I am thinking of deleting it in the future since it is not important.

## Step 4: Publish

In order to publish your page for free you need to upload your project to github. The easiset way to do so it to use VsCode.

1. Open your project in VsCode
2. Go to `Source Control` (3rd icon on the left)
3. Press `initialize repository`
4. Then write a commit message and press Commit
5. Choose public repo when prompted to select
6. Go to your github profile
7. Press Repositories
8. Choose your repo
9. Go to settings
10. Pages
11. Build and Deployment --> Chooose GitHub actions
12. Branch `main`
13. Press actions on the top left
14. Search for jekyll
15. Press `configure` on jekyll

Finito! Your blog will be published on `https://<your-github-name>.github.io/blog`
Now you can add new posts, modify your pages and whenever you push to your main branch it will update your blog.

Hope this tutorial helps you create your first blog 😊

## Sources

Below I summarize all my sources

- [Jekyll Documentation](https://jekyllrb.com/)
- [jekyllthemes.io](https://jekyllthemes.io/)
- [Template I am using](https://github.com/StartBootstrap/startbootstrap-clean-blog-jekyll)
