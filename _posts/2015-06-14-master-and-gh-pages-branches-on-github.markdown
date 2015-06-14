---
layout: post
title:  "Master and gh-pages in Github: keep your code and website in the same repo"
date:   2015-06-14 16:11:00
categories: post
---
<span class="leftImage imgDiv"><img alt="The reason" src="/assets/master-and-gh/00_intro.jpg" width="405/"></span>
Code and website in one repository : 2015 did not give us *“Back to the Future”* hoverboards, but it gave us the ability to put our websites next to our code on GitHub. However, doing it so is still easier said than done. In theory, this should be a one-click operation. But in practice, you need to be a little patient, understand a few git concepts and type in a small book on the command-line. And of course, you can skip all this and fork the template I created in this post which lives at [gh-pages-orphan-branch-template](https://github.com/byuksel/gh-pages-orphan-branch-template).

**Creating a repo for your code**

As of June 2015, you still cannot do this on the command line for GitHub. You can do it on the website or if you are over zealous, you can use the API with a RESTful client. For now, let’s say you like the simpler approach and do it on the website. First login to your account, and then click on this link and create your repository:

>[https://github.com/new](https://github.com/new)

Let’s call your username `<user>`,and your repository name `<repo>`. In the commands below, replace `<user>` with your actual username, and actual repository with `<repo>`.

<!--more-->

**The “master” branch**

Your code will live on the master branch. By default, everything you check-in to your repository lives in the master branch. Since we created the repository on the website, there is nothing in it. First, we need to configure a directory on your computer to represent your master branch. In other words, we will “clone” your master branch into a directory.

{% highlight bash %}
cd /project-directory
git clone --branch master  http://github.com/<user>/<repo>.git  <repo>-master
{% endhighlight %}

Let’s add a simple python file, and push it to the repository.

{% highlight bash %}
cd <repo>-master
echo "print 'Hello World!'" > helloworld.py
{% endhighlight %}

This creates helloworld.py in `<repo>-master` directory.

{% highlight bash %}
git add helloworld.py
{% endhighlight %}

This adds helloworld.py to the “to-be-commited” list. This is also called “staging”.

{% highlight bash %}
git commit -m "Committing helloworld.py"
{% endhighlight %}

Commits helloworld.py to your computer’s local git repository.

{% highlight bash %}
git push origin master
{% endhighlight %}

Pushes (uploads) the committed files to your repository’s master branch on GitHub. It also configures all the following “git pull/push” commands in this directory to track “master” branch only.

**The “gh-pages” branch**

Your website will live on the “gh-pages” branch. As a branch, gh-pages branch is different from other branches for two reasons. First, whatever you check-in will be served as a website (instead of a repo view) at a predefined url (or a custom url if you like). Second, you can use Jeykll to manage your content, and use this website as a blog.

We have to be careful while setting the gh-pages branch because we want the code to be on its own branch (in our example the master branch) and the website to be on another branch (this would gh-pages branch), while they are still in the same repository. We can accomplish this by making gh-pages an orphan branch, i.e a root-less branch. By default, branches have roots. In normal use cases, branches are created to make a set of changes to the same content that their roots contain. However, for our purposes we don’t want our website to be in the same branch as the code.

We can create gh-pages branch from the command-line. And the commands for creating such a rootless branch is a little confusing. You first clone your master branch into a new directory, and then set this as a new “orphan” branch. Then, you delete everything in the directory and add new content to check it into your new branch. It would have been a lot better if this could be done in one command, sigh!

{% highlight bash %}
cd <project-directory>
git clone --branch master  http://github.com/<user>/<repo>.git  <repo>-gh-pages
{% endhighlight %}

We now cloned the master branch into a directory named `<repo>-gh-pages`.

{% highlight bash %}
cd <repo>-gh-pages
git checkout --orphan gh-pages
{% endhighlight %}

This creates an orphan branch for our project with all the files from master branch still existing in the `<repo>-gh-pages` directory.

{% highlight bash %}
git rm -Rf .
{% endhighlight %}

This deletes everything that was left over from the master branch. Let’s now add a simple html file and check it into gh-pages branch.

{% highlight bash %}
echo "This is my webpage" > index.html
git add index.html
git commit -m "First gh-pages checkin"
{% endhighlight %}

Finally, let’s push the local changes in the “gh-pages” branch to our repository on GitHub.

{% highlight bash %}
git push origin gh-pages
{% endhighlight %}

“origin” tells git command that we want to talk to GitHub repository. It is a variable that is created when we used “git clone” command and it has the repository value we used in “git clone”. “Gh-pages” is the branch we want this directory to track. In other words, when we push, we want only the changes to the “gh-pages” branch to be pushed from this directory. Confusing? yes! But alas, it works! Once you execute this command, all future “git push” commands from this directory will use the same configuration.

{% highlight bash %}
git branch -r
{% endhighlight %}

This command will show all the branches on your GitHub repository, a.k.a. “remote”. It should print something like this:


|  origin/HEAD -&gt; origin/master 
|  origin/gh-pages 
|  origin/master 

<br>

In your `<project-directory>`, you now have 2 separate directories which map to two separate branches. `<project-directory>/<repo>-master` maps to **“master”** branch `<project-directory>/<repo>-gh-pages` maps to **“gh-pages”** branch

**Your webpage**

Your webpage will be available at `http://<user>.github.io/<repo>`. When you go to this link, you should see:

{% highlight html %}
This is my webpage.
{% endhighlight %}

Have fun with master and gh-pages branches!!!



