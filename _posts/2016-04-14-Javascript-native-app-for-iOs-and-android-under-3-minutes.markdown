---
layout: post
title:  "Javascript iOS and Android app under 3 minutes"
date:   2016-04-14 00:08:00
comments: true
categories: post
---
<span class="leftImage imgDiv"><img alt="The reason" src="/assets/cordova/00_intro.png" width="405/"></span>"Write code once in one language for an app, and run it on both iOS and Android." If I could have one mediocre super power, I would want that. Imagine how wonderful it would be if you could build a phone app that can run on iOS or Android without learning any of the gimmicks of either app enviorment. The engineers working on Apache's Cordova must have had the same thought.


[Cordova](cordova.apache.org) is an open source framework from Apache that enables you to use Javascript, HTML and simple CSS to build your app, and compile it into any of these mobile platforms, and immediately start running the app. It is not perfect, it does not have all the bells and whistles of both platforms. However, it does a wonderful job for most of the part. 

Cordova is a fantastic tool to quickly prototype apps. We can build a simple app for both platforms in less than 3 minutes. 
<!--more-->

**Installation**

First we will need to install Cordova using [npm](http://npmjs.com)

{% highlight bash %}
npm install cordova -g
{% endhighlight %}

If you are going to use *iOS*, you will need to make sure that you have installed *XCode*.

If you are going to use *Android*, you should install [Android SDK](http://www.google.com/search?q=andorid+sdk). You need to make sure `android` is accessible on your command line.

**Creating your first app**

Now that you have cordova, let's create an app. 


{% highlight bash %}
 cordova create <name-of-the-app-directory> <reverse-com-name> <app-name>
{% endhighlight %}

For example, let's create an app called 'ButtonMe' under the directory named myapp:

{% highlight bash %}
 cordova create myapp com.baris.myapp ButtonMe
{% endhighlight %}

This will create the directory called 'myapp' with a sample app in it. Let's now add support for Android.

{% highlight bash %}
 cd myapp
 cordova platform add android
{% endhighlight %}

Let's also add support for iOs.
{% highlight bash %}
 cordova platform add ios
{% endhighlight %}

**Creating and Starting Your Android Emulator**

Type `android` on your commandline. This should start 'Android SDK Manager'. Click 'Tools' and 'Manage AVDs'. Click on 'Create' to create a new *Android Virtual Device* and then 'Start' to start it so that Cordova can use it.

'Android SDK Manager' is a continously developed product. I won't be giving instructions on how to create your AVD as it may be obsolute very quickly. Instead please follow the most up-to-date documentation on Android's site to create and start your AVD.

**Your first app**

The gist of Cordova is to design and build everything as a Single Page Application. You should update the html of your single page dynamically if you want to have multiple pages. 

*index.html* (under `myapp/www/index.html`) and *index.js* (under `myapp/www/js/index.js`  are going to be the basic building blocks of our app. We will use index.html to create the layout of our app and *index.js*.  

Let's add a button to our index.html file. 
{% highlight html %}
<div class="app">
  <h1>My BEAUTIFUL APP</h1>
  <button id="mybutton"> HO-HO BUTTON</button>
  <div id="deviceready"></div>
</div>
{% endhighlight %}

And let's modify index.js to add these lines:

{% highlight javascript %}
var count = 0;

document.getElementById('mybutton').addEventListener('click', pressed, false);

function pressed() {
    count++;
    document.getElementById('deviceready').innerHTML = 'You clicked me ' + count + ' times. YAY!';
}
{% endhighlight %}


**Your first app on emulators**

Let's send this app to Android and iOS emulators:
{% highlight bash %}
 cordova emulate android
 cordova emulate ios
{% endhighlight %}
<div class="outerDiv">

<div class="imgDiv"><img alt="The reason" src="/assets/cordova/01_android.png" width="405/"></div>

<div class="imgDiv"><img alt="The reason" src="/assets/cordova/02_iphone.png" width="405/"></div>
</div>

