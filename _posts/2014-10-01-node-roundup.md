---
layout: post
title: "Node Roundup: Node 0.11.14, svgexport, node-webkitgtk"
author: "Alex Young"
image: "/images/posts/libuvdinosaur.png"
categories:
- modules
- libraries
- node
---

###Node 0.11.14

![libuv](/images/posts/libuvdinosaur.png)

[Node 0.11.14](http://blog.nodejs.org/2014/09/24/node-v0-11-14-unstable/) has been released, with updates for uv, http_parser, npm, openssl, and v8.

There seem to be fixes for almost every core module: cluster has been reverted to the 0.10 `setupMaster` behaviour, `console.dir` accepts options, events now outputs the event that is leaking -- there are loads more changes that you should be aware of before updating.

The version of uv included in 0.11.14 is rc1.  Also, when I went to check the recent commits for uv I noticed it now has a cool dinosaur/unicorn logo.

###svgexport

svgexport (GitHub: [shakiba / svgexport](https://github.com/shakiba/svgexport), npm: [svgexport](https://www.npmjs.org/package/svgexport)) by Ali Shakiba is a command-line tool for converting SVG files to PNG, JPEG, and PDF.

It's based on PhantomJS, and the author has been using it to automatically convert icons for iOS and Android projects.  This seems like a cool use for Node/Gulp/Grunt as part of a non-web-native build chain that I hadn't thought of before.

###node-webkitgtk

node-webkitgtk (GitHub: [kapouer / node-webkitgtk](https://github.com/kapouer/node-webkitgtk), License: _MIT_, npm: [webkitgtk](https://www.npmjs.org/package/webkitgtk)) by Jérémy Lal is a set of webkitgtk bindings for Node.  The API is chainable, so you can do things like this:

{% highlight javascript %}
WebKit().load('http://github.com').png('github.png').pdf('github.pdf')
{% endhighlight %}

It's designed to be used headlessly, so it's useful for things like generating website thumbnails, or maybe integration testing but I haven't tried that.

