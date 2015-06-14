---
layout: post
title:  "Emacs on steroids for Python: elpy.el"
date:   2014-03-06 23:15:00
categories: post
---
<span class="leftImage imgDiv"><img alt="The reason" src="/assets/emacs-on/00_intro.jpg" width="405/"></span>
You may have no problem programming Python in naked Emacs out of the box. But you may also know that with Emacs, there is always more. Just like the way Popeye would pop a can of spinach down his stomach to boost his act into a super human being’s, you can install a few tiny packages to transform Emacs into a super Python IDE. You won’t regret feeding these supplements to your Emacs, because once you set them up, you will never go back.

Elpy.el mode is the lead actor here, with jedi and rope are in the supporting roles. After installing these three packages, you get everything you wish for from a nice Python IDE: auto-complete, snippet expansion, syntax error highlighting, lint-like pep8 highlighting, indentation highlighting, simultaneous editing, easy code block shifting.

Elpy.el mode itself is a conglomerate of many other packages each of which brings yet another greatness onto the table.

**Auto-complete**

Emacs will complete the commands you started typing when you hit `TAB`. If there are multiple possible completion patterns, it will show the choices as well as the descriptions.

`TAB` becomes a powerful key with elpy.el mode. For example, type “whi” and hit `TAB`, elpy completes it to “while”. Type “ope”, hit `TAB`, elpy mode completes it to “open” and shows you the definition of open() method. Auto-complete is brought in by jedi and rope.
s
<!--more-->

<div class="outerDiv">
<div class="imgDiv"><a href="/assets/emacs-on/01_emacs_big.png">
<img alt="image" src="/assets/emacs-on/01_emacs.png">
</a></div></div><br>

**Snippet Expansion**

Type *"for"* and hit `C-c k`. You will now see the standard template for a *"for"* loop in Python and all you have to do is to fill in the blanks. Type *"def"*, hit `C-c k` and you will be looking at the template for a Python methods. Snippet expansion automatically writes up the template for you. Snippet expansion is brough in by **yasnippet.el**.

<div class="outerDiv">
<div class="imgDiv"><a href="/assets/emacs-on/02_emacs_big.png">
<img alt="image" src="/assets/emacs-on/02_emacs.png">
</a></div></div><br>

**Syntax Error Highlighting and PEP8 Highlighting**

Elpy.el mode also installs **flymake.el** which is an indispensable aid: it highlights the lines that have syntax errors or do not fit the pep8 guidelines. In other words, any error or any typing style that is deemed undesirable by Python Foundation will be highlighted in red. Flymake runs the checks on the fly, it will mark things as you save the file.

By the way, it is a good habit to follow the PEP8 suggestions. It will make your code more readable, and will make bugs easier to notice.

<div class="outerDiv">
<div class="imgDiv"><a href="/assets/emacs-on/03_snippet_big.png">
<img alt="image" src="/assets/emacs-on/03_snippet.png">
</a></div></div><br>

**Indentation Highlighting**

Elpy will show you how many `TAB`s there are in the beginning of each line. This helps with the most notorious Python bugs: mis-indented code blocks. You can type `M-x highlight-indendation-mode` to turn off (or on) if these highlights annoy you too much.

**Simultaneous Editing**

Let’s say that you have a variable called "my_var". And you used this variable in many many places. All of a sudden you realize that "my_var" is a pretty cryptic name and you want to rename it to "my_var_that_holds_sum". With simultaneous editing, you can edit all "my_var" variables in one action: go over one of the "my_var"s and hit `C-c o`. Then, type away. You will see that all the variable names are getting updated as you type.

<div class="outerDiv">
<div class="imgDiv"><a href="/assets/emacs-on/04_editing_big.png">
<img alt="image" src="/assets/emacs-on/04_editing.png">
</a></div></div><br>

**Code block shifting**

If you want to move a block of code one `TAB` to the right or left, all you have to do is to type `C-c >` or `C-c <` respectively.

**How do you do it?**

**1. Install elpy, jedi and rope on your computer**

Go to your terminal, and type

{% highlight bash %}
sudo pip install elpy jedi rope
{% endhighlight %}

If you don’t have *"pip"*, assuming you have Macports, you can install it with *"port"* by typing

~~~
sudo port install pip
~~~

**2. Install elpy.el and flymake-cursor.el on your Emacs**

We are going to use package.el mode. You need to have Emacs 24 or later. Add “marmalade” to your package repositories in your .emacs file by adding this line:


{% highlight lisp %}
(require 'package)
(add-to-list 'package-archives
'("marmalade" . "http://marmalade-repo.org/packages/"))
{% endhighlight %}

Hit `M-x package-install-packages`, search for elpy by typing C-s elpy. Hit “I” to select, and then hit “X” to execute the installation. Package mode now should install about 12 packages.

Syntax error highligthing shows what error it is when your hover over your mouse on the error. But you can also get this message at the cursor. If you want this(this is optional), we need to do the same thing for flymake-cursor mode. Hit C-s flymake-cursor, hit “I” and then “X” to install the package.

**3. Add configuration lines to your .emacs**

Add these two lines to your .emacs file.

{% highlight lisp %}
(package-initialize)
(elpy-enable)
{% endhighlight %}

**4. Fix 2 bugs with keybindings**

Unfortunately, elpy.el came with 2 bugs for my installation: the keybindings for snippet expansion and simultaneous editing did not work. I had to change these bindings in the .emacs file. I picked the keybinding C-c k for snippet expansion and C-c o for simultaneous editing. They are ultimately random. You can change them if you like. So, for now, just add these two lines to your .emacs file after (elpy-enable) line:

{% highlight lisp %}
;; Fixing a key binding bug in elpy
(define-key yas-minor-mode-map (kbd "C-c k") 'yas-expand)
;; Fixing another key binding bug in iedit mode
(define-key global-map (kbd "C-c o") 'iedit-mode)
{% endhighlight %}

**5. Make sure PYTHONPATH is set correctly**

We need to make sure that `PYTHONPATH` environment variable is set correctly for elpy to work. At the console, type:

~~~
echo $PYTHONPATH
~~~

This should print where your Python executable resides. If not, first find out where your Python path is:

~~~
which python
~~~

And whatever the output is, add this line to your .emacs

{% highlight lisp %}
(setenv "PYTHONPATH" "the_path_which_python_command_returned")
{% endhighlight %}

You should be good to go. Restart your Emacs and open a Python file, and code away!!!

Here is the short video for the installation instructions:

<div class="outerDiv">
<div class="imgDiv"><iframe class="video" frameborder="0" height="315" src="//www.youtube.com/embed/0kuCeS-mfyc" width="560"></iframe></div>
</div>

<br>
And another short video for the usage instructions this time:

<div class="outerDiv">
<div class="imgDiv"><iframe frameborder="0" height="315" id="video" src="https://www.youtube.com/embed/mflvdXKyA_g" width="560"></iframe></div>
</div>

Links:

1. Big kudos to Jorgen Schäfer who coded up Elpy Mode. It used to be a big pain in the back to install all these packages seperately. But now, it literally takes minutes to get them all. Thank you again!“Elpy Mode”
2. PEP8 or Style Guide for Python from Python Foundation is awesome. PEP8
