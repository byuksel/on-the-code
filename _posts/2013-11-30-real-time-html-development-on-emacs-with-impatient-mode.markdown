---
layout: post
title:  "Real-time Html Development on Emacs with Impatient Mode"
date:   2013-11-30 13:18:00
categories: post
---
<span class="leftImage imgDiv"><img alt="The reason" src="/assets/real-time-html/00_intro.png" width="405/"></span>
With the rise of [jsfiddle.net](http://jsfiddle.net) and [jsbin.com](http://jsbin.com), the power of seeing how your html, css and javascript look together on a browser instantly just as you type is now available to the masses. Their popularity is already proving the point: it is much faster and more robust to develop in this manner. However, they both fall short of being the preferred tool for large projects with multiple files.

Would it not be great if you can use Emacs in a similar fashion to jsfiddle, i.e. just as you type into Emacs, you would be able to see it on the browser how the website renders real-time.

As it turns out, Emacs already supports this, and it is called the “impatient plugin”. In order to get it working though, you have to set it up. The plugin will start a local web server, and will serve the document you are editing to the browsers on your computer continuously. And once you taste the feel of immediate feedback, I can tell you that you will never go back.

Here are the steps to get the impatient mode on Emacs:

<!--more-->
<br>
**1. Modify your ~/.emacs file**

You can use ‘package’ command to install the impatient mode. “package” already comes together with Emacs 2.4 (or newer). The other option is to install it from the source code, but that is not what I did. In order to run “package” correctly, you need to change your .emacs file (which resides under your home directory) and add these 3 lines.

<div class="outerDiv">
<div class="imgDiv"><img alt="image" src="/assets/real-time-html/01_emacs.png"></div>
</div><br>

**2. Upgrade your Emacs (if you need to)**

After you add the lines, you need to restart Emacs. When I did so, I got an error message: I did not have “package”. Turns out that I had an older version of Emacs, so I needed to upgrade it to the most recent version. I decided to use MacPorts. After Google’ing and installing the macports pkg, all I had to do was to type “sudo port install emacs”, and voila. I had Emacs 24.3 on my computer.

<div class="outerDiv">
<div class="imgDiv"><img alt="image" src="/assets/real-time-html/02_macports.png"></div>
</div>

<div class="outerDiv">
<div class="imgDiv"><img alt="image" src="/assets/real-time-html/03_macports.png"></div>
</div><br>


**3. Install “impatient” mode with “package”**

Once I started my new Emacs version, everything was working fine. You type M-x package-list-packages, and “package” downloads the list of packages from MELPA. Next, you have to search for Impatient (Ctrl+S Impatient), mark it with “I”, and hit “X” to download and install “impatient” mode.

<div class="outerDiv">
<div class="imgDiv"><img alt="image" src="/assets/real-time-html/04_impatient.png"></div>
</div><br>

**4. Start httpd and impatient modes**

At this point, you have MacPorts, a new Emacs version, “package” and “impatient mode”. You did go through all this trouble to finally start your awesome mode. First, run “httpd-start” mode by typing M-x httpd-start. And then, run “impatient mode” by typing M-x impatient.

**5. Enjoy your realtime html rendering**

Start a new html file: I named mine temp.html. Open up your browser and go to “http://localhost:8080/imp”. You should see a list of all the Emacs buffers you are editing. If you also called your file temp.html, click on it. Now, as you type in Emacs, the changes will show automatically on the browser real-time. If you like, you can open different browsers such as IE or Firefox and navigate to the same location. All browsers will change you type in to temp.html.

<div class="outerDiv">
<div class="imgDiv"><img alt="image" src="/assets/real-time-html/05_public.png"></div>
</div>
<div class="outerDiv">
<div class="imgDiv"><img alt="image" src="/assets/real-time-html/06_emacs.png"></div>
</div><br>


The real-time immediate feedback really improves the development cycles as well as speeding them up. Have fun with it!

And voila, here is the short video for instructions:

<div class="outerDiv">
<div class="imgDiv"><iframe frameborder="0" height="315" id="video" src="//www.youtube.com/embed/mnfPRLlsXqU" width="560"></iframe></div>
</div><br>

Links

1. MacPorts makes it really easy to install open source projects on your mac.
2. MELPA is a package archive for Emacs. If you install “package”, you can easily manage your Emacs packages.
3. Impatient mode is the topic of this post. It is awesome.

*Baris Yuksel*
