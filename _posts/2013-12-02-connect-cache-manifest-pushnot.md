---
layout: post
title: "connect-cache-manifest, pushnot"
author: "Alex Young"
categories: 
- express
- node
- apps
---

###connect-cache-manifest

connect-cache-manifest (GitHub: [dai-shi / connect-cache-manifest](https://github.com/dai-shi/connect-cache-manifest), License: _BSD_, npm: [connect-cache-manifest](https://npmjs.org/package/connect-cache-manifest)) by Daishi Kato is Express middleware for generating a HTML5 cache manifest file.  Manifests basically list the files needed by the application when it's offline, so any essential client-side assets can be cached by the browser.

Daishi's middleware takes an object and then generates a suitable manifest file.  It can recurse through directories so including lists of JavaScript, CSS, and images is easier.

{% highlight javascript %}
app.use(cacheManifest({
  manifestPath: '/application.manifest',
  files: [{
    file: __dirname + '/public/js/foo.js',
    path: '/js/foo.js'
  }, {
    dir: __dirname + '/public/css',
    prefix: '/css/'
  }, {
    dir: __dirname + '/views',
    prefix: '/html/',
    ignore: function(x) { return /\.bak$/.test(x); },
    replace: function(x) { return x.replace(/\.jade$/, '.html'); }
  }],
  networks: ['*'],
  fallbacks: []
}));
{% endhighlight %}

###pushnot

![pushnot](/images/posts/listjs-logo.png)

[pushnot](http://me.dt.in.th/page/pushnot/) (GitHub: [dtinth / pushnot](https://github.com/dtinth/pushnot), License: _MIT_) by Thai Pangsakulyanont is a push notification server based on ØMQ, Express, and Zephyros.  It supports notification encryption and can be hooked up to Growl.

> Pushnot consists of three major components:
> The server that clients can send a notification to, and subscribers can subscribe to these notifications.
> The client is any application that wants to send a notification to the user.
> The subscriber waits for the server to push the notification and notifys the user.

It's got an interesting mix of technologies, if you're looking for an Express application that uses pub/sub, and it has a command-line interface as well.
