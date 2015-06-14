---
layout: post
title:  "iMovie Fail: Very slow importing, iMovie'11 and h264"
date:   2014-01-14 08:47:00
categories: post
---
<span class="leftImage imgDiv"><img alt="The reason" src="/assets/imovie-fail-very-slow/00_intro.png" width="405/"></span>
iMovie sometimes takes a really really long time to import a relatively small clip encoded in “h264”. For example, a 50 second clip can take up to 10 minutes to import, while a similar clip of the same duration with an ”mpeg4” encoding would take only seconds. If you are going to import a medium size movie, you are ultimately out of luck. For a 20 minute clip, iMovie can take up to 6 hours.

After a little experimentation, the source of the problem materialized itself on my computer screen like a dew drop on a lotus leaf. “h264” is a interframe codec. It can use information from other frames to encode a certain frame. This potentially decreases the size of encoded of video while maintaining the quality. However, iMovie’11 cannot edit a file encoded in an interframe encoding: in order to edit a frame, there should be no inter dependency across other frames. iMovie should be able to manipulate a frame independent of others in a clip. Hence, iMovie reencodes the movie in “iCod” (a Quicktime format), and this takes a really long time while requiring a great deal of free drive space.

There is a neat solution to all this mess. You can re-encode your video in “h264” with exactly the same settings but by only turning off inter frame lookups. This process will create a video with visually no quality degradation and very little increase in the size. And, iMovie will be able to import your movie quickly.

“ffmpeg” command line tool enables you to use “h264” with no inter frame lookups. You need to use “-preset ultrafast” to accomplish this. In my example,

<!--more-->

~~~
ffmpeg -i DSCN3013.MOV -strict -2 -c:v libx264 -preset ultrafast DSCN3013_fast_decode.MOV
~~~

* “-c:v:libx264” sets the encoder to h264
* “-preset ultrafast” turns off inter frame lookups. This is where the magic lies.
* “-strict -2” was suggested by ffmpeg. Since my movie’s audio was encoded in AAC, I had to use this setting.
* If you want to keep the bitrate the same as the original file, you have to first check the bitrate of the original file with:

~~~
ffmpeg -i DSCN3013.MOV
~~~

The output will have a line like this:

> Stream #0:0(eng): Video: h264 (Main) (avc1 / 0x31637661), yuvj420p, 1280x720 [SAR 1:1 DAR 16:9], 8283 kb/s, 29.97 fps, 29.97 tbr, 30k tbn, 59.94 tbc

This tells me that the movie was encoded with 8283kb/s. So, I added “-b:v 8283k” to the ffmpeg line. My final command line was this:

~~~
ffmpeg -i DSCN3013.MOV -strict -2 -c:v libx264 -preset ultrafast -b:v 8283k DSCN3013_fast_decode.MOV
~~~

<div class="outerDiv">
<div class="imgDiv"><a href="/assets/imovie-fail-very-slow/01_ffmpeg_big.png">
<img alt="image" src="/assets/imovie-fail-very-slow/01_ffmpeg.png">
</a></div></div><br>


I have always been baffled by how badly iMovie is designed for errors. There is no explicit communication of what is happening and no course of action is ever offered should you run into a problem. Design world has known it better since 1980s than the Apple iMovie engineers know in 2010s.

