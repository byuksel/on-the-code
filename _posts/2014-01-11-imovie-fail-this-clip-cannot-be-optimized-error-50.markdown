---
layout: post
title:  "iMovie Fail: \"This clip cannot be optimized. Error -50\""
date:   2014-01-11 09:08:00
categories: post
---
<span class="leftImage imgDiv"><img alt="The reason" src="/assets/imovie-fail-this-clip/00_intro.png" width="405/"></span>
iMovie sometimes simply cannot implement “fast forward” or “slow motion” on movie clips. This happens when you have a project in which you want to edit part of a movie to play at higher speeds such as 2x, 4x, etc (or at lower speeds for that matter). iMovie will tell you that it will need to optimize the clip before you can fast forward it, and then it will fail with a cryptic message: “This clip cannot be optimized. Error: -50”

It turns out that the problem is unambiguous, you just don’t have enough space on your drive for the optimization. If you have multiple drives, this would be the drive on which you created the “Event” when importing your clip.

Evidently, the remedy is simple, just create more space on your drive. But, what if you cannot do that? There is an alternative, you can decrease the size of your clip by reducing the “bitrate” using a command line tool called “ffmpeg”. Of course, you will have to do this before importing your movie to iMovie.

Here are the steps:

<!--more-->

**1. Failed to import with optimization on iMovie on “Import Movies…”**

The movie I had was 1.65 Gigs, and I had 3.5 Gigs empty on my hard drive. For iMovie, this was just not enough for optimizing the video. It would fail without any error messages.

<div class="outerDiv">
<div class="imgDiv"><img alt="image" src="/assets/imovie-fail-this-clip/01_imovie.png"></div>
</div><br>

Since this failed, I unchecked the “Optimize video” and imported the movie without any optimization.

**2. Failed to optimize the clip when trying to “Fast Forward”**

When I tried to “fast forward” the clip, iMovie said that “the clip must be converted before its speed can be adjusted”. When I ok’ed that, it started “optimizing”, only to fail with the ever famous cryptic message: “This clip cannot be optimized. Error: -50”

<div class="outerDiv">
<div class="imgDiv"><img alt="image" src="/assets/imovie-fail-this-clip/02_fail.png"></div>
</div><br>

**3. What to do next?**

I could not delete more files, so I decided to lower the bitrate of my video to decrease the size. “ffmpeg” can do this easily.

**4. Install ffmpeg using MacPorts**

I decided to use MacPorts to install “ffmpeg”. After Google’ing and installing the macports pkg, I opened “Terminal” and typed “sudo port install ffmpeg”. Voila, I had ffmpeg on my computer. You can use Command + Space to open the search bar on the top right, and type “Terminal” to find Terminal on your Mac.

<div class="outerDiv">
<div class="imgDiv"><img alt="image" src="/assets/imovie-fail-this-clip/03_macport.png"></div>
</div><br>

<div class="outerDiv">
<div class="imgDiv"><img alt="image" src="/assets/imovie-fail-this-clip/04_install.png"></div>
</div><br>

**5. The command line**

First you have to change to the directory that the movie resides in. For my case, it is in “~/Document”. I typed “cd ~/Documents”. Then, I wanted to check what the movie is encoded in. I typed “ffmpeg -i MOVIE_FILENAME”. This will tell you the encoding, and the bitrate. My file was encoded in h264 with 8147k bitrate. I decided to halve the bitrate to 4000k. So I typed:

~~~
ffmpeg  -i INPUT_FILENAME -strict -2 -b:v 4000k -c:v h264 -preset superfast OUTPUT_FILENAME
~~~

Couple points to pay attention to:

* `“-b:v 4000k”` sets the output bitrate 4000k, while “-c:v h264” sets the encoder for video to be h264.
* Since my movie’s audio was encoded in AAC, ffmpeg asked me to add “-strict -2” to the command line. I did that.
* When I first tried to use “-c:v h264”, iMovie’s optimization on ffmpeg’s output would take forever and the optimized file would be many times larger than the original, which beats my purpose. After a bit tinkering, I found out that you need to disable h264’s interframe reference by adding the setting to “-preset superfast”

<div class="outerDiv">
<div class="imgDiv"><img alt="image" src="/assets/imovie-fail-this-clip/05_ffmpeg.png"></div>
</div><br>

**6. Success!**

The output file was only 800 Megs with not so much of a difference in quality, at least for my purposes. And iMovie successfully optimized the new video.

It comes as a surprise how horrific iMovie is designed for errors. On one hand iMovie is an immensely user-friendly tool for quick editing your movies. But on the other hand, it does not go much further in error handling than the long-gone DOS operating system with its own version of cryptic error messages. From a design perspective this is one of the no-no’s in Donald Norman’s monumental “Design of Everyday Things”. In his book, Norman gives a simple recipe for ‘how to do things wrong’ and I believe iMovie engineers followed these instructions really well, especially the fourth bullet point:

*`Use idiosyncratic language or abbreviations. Use uninformative error messages`*(1)

Once you finish editing your movie, I strongly recommend to add Norman’s book to your reading list. It is quick and very informative.



Links:

1. Donald Norman, “Design of Everyday Things” (2002), page 179

 
