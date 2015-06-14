---
layout: post
title:  "How to download multiple files from your phone over wifi (Android)"
date:   2013-10-30 15:21:00
categories: post
---
<span class="leftImage imgDiv"><img alt="The reason" src="/assets/how-to-download/00_phone_photo.png" width="405/"></span>
You might be one of those who just loves doing everything over the air, or you might be like me who owns an Android phone with a broken usb port. Whatever your reason is, you already are aware that it is a pain in your gut to download a bunch of photos at once over a wireless connection. You might choose to send yourself an email with your photos attached by manually selecting one at a time, or you might try bluetooth. I will guarantee you that both of these methods will only help to turn your hair grey faster. In fact, try sending a video, you will turn into an old human being very quickly.

Behold, there is a solution. There indeed exists a super fast way to download (or upload) whatever you want over a wireless connection. Simply put, you can install a light-weight FTP server on your phone and then, transfer any file at the speed of your wireless router.  For me, it took about 2’ 33” for a 69Mb file. This corresponds to less than a second transfer rate per second of movie I shot with my settings for mp4 videos.
<!--more-->

**1.Install a light-weight FTP-server.**

I chose to install the demo version of the FTP server written by Pietr Parait. You can search it on your phone’s Google Play store, and download. Or you can scan the QR code below with your phone (using Barcode Scanner).

<div class="outerDiv">
<div class="imgDiv"><img alt="image" class="midImage" src="/assets/how-to-download/01_qr_code.png"></div>
</div>

**2.Start the server on your phone**

Click “Running” and then your server starts on 192.168.0.12 port 2121 (your values could be different than mine). You can also set your username and password for your ftp client to login.

<div class="outerDiv">
<div class="imgDiv"><img alt="image" class="midImage" src="/assets/how-to-download/03_ftp_server.png" width="305"></div>
</div>

**3.Install an FTP client to your computer**

You can either go the old school way and use your command-line ftp client that comes with your Mac, or you can treat yourself to a nice user experience. I installed FileZilla from FileZilla Project.

<div class="outerDiv">
<div class="imgDiv"><img alt="image" class="midImage" src="/assets/how-to-download/04_filezilla.png"></div>
</div>

**4.Connect and download**

Enter your server address and port from (2) along with your username and password. Click `Quickconnect`. You are now a proud owner of a phone which avails its data on your local network to your computer.
Have a great downloading time, and save yourself from getting gray hair,

And voila, here is the short video for instructions:

<div class="outerDiv">
<div class="videoWrapper">
<iframe frameborder="0" class="video" src="//www.youtube.com/embed/kpc7Y-au7Gg"></iframe>
</div></div>
