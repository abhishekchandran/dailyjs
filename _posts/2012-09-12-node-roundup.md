---
layout: post
title: "Node Roundup: 0.8.9, xmlson, Mubsub, Book on libuv"
author: "Alex Young"
categories:
- node
- modules
- libraries
- books
- xml
- json
- pubsub
---

<div class="intro">
You can send in your Node projects for review through our <a href="/contact.html">contact form</a> or <a href="http://twitter.com/dailyjs">@dailyjs</a>.
</div>

###Node 0.8.9

[Node 0.8.9](http://blog.nodejs.org/2012/09/11/node-v0-8-9-stable/) is out, and this looks like a significant release judging by the long changelog.  v8, npm, and GYP have all been updated, and there are quite a few platform-specific bug fixes relating to memory.

###xmlson

[xmlson](https://github.com/wearefractal/xmlson) (License: _MIT_, npm: [xmlson](https://npmjs.org/package/xmlson)) by the developers at Fractal is a libexpat-based XML/JSON conversion module:

{% highlight javascript %}
var xmlson = require('xmlson');

xmlson.toJSON('<p><h1 title="Details">Title</h1></p>', function(err, obj) {
  // Do something with obj
  console.log(obj.p.h1)
});
{% endhighlight %}

In the previous example, `[ { '@title': 'Details', text: 'Title' } ]` will be printed, so attributes are included when converting to JSON.  There's also a synchronous API.  Installing xmlson with npm will compile the necessary dependencies with gyp.

This module is a fairly lightweight wrapper around [ltx](https://npmjs.org/package/ltx), which is worth checking out.

###Mubsub

[Mubsub](https://github.com/scttnlsn/mubsub) (License: _MIT_, npm: [mubsub](https://npmjs.org/package/mubsub)) by Scott Nelson is a publish–subscribe implementation that uses MongoDB:

> It utilizes Mongo's capped collections and tailable cursors to notify subscribers of inserted documents that match a given query.

To use it, a channel must be created and then subscribed to.  It can work with MongoDB connection URLs, so it's fairly easy to drop into an existing MongoDB-based Node project.  It comes with Mocha/Sinon.JS tests.

###Book: An Introduction to libuv

[An Introduction to libuv](http://nikhilm.github.com/uvbook/) by Nikhil Marathe is a guide to libuv.  It covers streams, threads, processes, event loops, and utilities.  If you're trying to understand what makes Node different, and how its asynchronous and event-based design works, then this is actually a great guide.  Try looking at [Basics of libuv: Event loops](http://nikhilm.github.com/uvbook/basics.html#event-loops) as an example.
