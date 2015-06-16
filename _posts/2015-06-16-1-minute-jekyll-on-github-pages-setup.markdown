---
layout: post
title:  "1-minute Jekyll on GitHub Pages setup"
date:   2015-06-16 00:08:00
comments: true
categories: post
---
I have one of the “fastest” recipes for setting up on a Jekyll blog on GitHub pages from command-line. And I hereby give this recipe to you. If you have Jekyll installed on your computer, it will take you less than 1 minute to set up your own website which you can manage with Jekyll. And of course, you can skip all this and fork the template I created in this post which lives at [gh-pages-orphan-branch-template](https://github.com/byuksel/gh-pages-orphan-branch-template).

The birdview process is this: we will first create a new Jekyll project using `jekyll new` command. This will create a bunch of files. To these files, we will add a file named "Gemfile" instructing Jekyll to install a few packages necessary for GitHub integration, and run an install command.  Then we will initialize this directory for git,  add a remote, and checkout the “gh-pages” branch.. Once we commit all the files and push to “gh-pages” branch, your website will be live on the internet hosted by GitHub.

<!--more-->

##1-minute Jekyll on GitHub Pages setup##

First login to your GitHub account on your browser, and then click on this link and create your repository:

>[https://github.com/new](https://github.com/new)

Let’s call your username `<user>`,and your repository name `<repo>`. In the commands below, replace `<user>` with your actual username, and actual repository with `<repo>`.


{% highlight bash %}
cd /project-directory
jekyll new <repo>-dir
cd <repo>-dir
{% endhighlight %}

This creates a new Jekyll project under `<repo>-dir` directory. Now, let’s add our “Gemfile” file, and run the install script for Github packages to be installed.

{% highlight bash %}
printf "source 'https://rubygems.org' \n gem 'github-pages'" > Gemfile
bundle install
{% endhighlight %}

If you don’t have “bundle” installed, you can run `gem install bundler`. All the files should be where they are now. You can check if things are working by running Jekyll in this directory with `jekyll serve’ and browsing to “localhost:4000”.

Let’s now push all the content to the “gh-pages” branch of GitHub.

{% highlight bash %}
git init
git remote add origin https://github.com/byuksel/gh-pages-orphan-branch-template.git
git checkout --orphan gh-pages
git add .
git push origin gh-pages
{% endhighlight %}

Voila, your website should be up at `http://<user>.github.io/<repo>`.
