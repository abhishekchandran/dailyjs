---
layout: post
title: "Node Roundup: 0.10.36, io.js 1.0.4, Object.observe, Shipit"
author: Alex Young
image: "/images/posts/shipit.png"
categories:
- node
- modules
- libraries
- iojs
- deployment
---

###Node 0.10.36, io.js 1.0.4

The latest stable release of Node, [0.10.36](http://blog.nodejs.org/2015/01/26/node-v0-10-36-stable/), came out earlier this week.  The changelog is short with just three bullets, but one thing that stands out is "v8: don't busy loop in cpu profiler thread".  The commit for this is [6ebd85](https://github.com/joyent/node/commit/6ebd85e10535dfaa9181842fe73834e51d4d3e6c):

> Before this commit, the thread would effectively busy loop and consume
> 100% CPU time.  By forcing a one nanosecond sleep period rounded up to
> the task scheduler's granularity (about 50 us on Linux), CPU usage for
> the processor thread now hovers around 10-20% for a busy application.

In [io.js](https://iojs.org/), 1.0.4 has been released.  I noticed in [the changelog](https://github.com/iojs/io.js/blob/v1.x/CHANGELOG.md) that there's a patch for V8 and ARMv6, so io.js should work again on platforms like Raspberry Pi.

###Object.observe

It seems like I've been writing about a lot of frameworks that use ES6/7, but sometimes you just want a specific polyfill rather than an entire framework.  A new polyfill that Massimo Artizzu sent me is for `Object.observe` (GitHub: [MaxArt2501/object-observe](https://github.com/MaxArt2501/object-observe), License: _MIT_, npm: [object.observe](https://www.npmjs.com/package/object.observe), Bower: _object.observe_), which you can use with Node and browsers.

The readme explains the basic usage, but there's also [more detailed documentation](https://github.com/MaxArt2501/object-observe/blob/master/doc/index.md).  This also explains the two versions of the API:

> If you don't need to check for "reconfigure", "preventExtensions" and "setPrototype" events, and you are confident that your observed objects don't have to do with accessor properties or changes in their descriptors, then go for the light version, which should perform reasonably better on older and/old slower environments.

In Node 0.10.x, you can use it like this:

{% highlight javascript %}
if (!Object.observe) require('object.observe');
{% endhighlight %}

This will avoid loading it when your version of Node gets `Object.observe` in the future.

###Shipit

![Shipit](/images/posts/shipit.png)

Greg Bergé sent in Shipit (GitHub: [shipitjs/shipit](https://github.com/shipitjs/shipit), License: _MIT_, npm: [shipit-cli](https://www.npmjs.com/package/shipit-cli)), a deployment tool.  It can use SSH to sign in to a server and run scripts, and it handles multiple environments so you can create settings that will work for production, staging, CI, and so on.

It has an event-based API with tasks, in a style that reminds me of Grunt and Gulp. It uses plain old SSH and rsync under the hood.

Shipit recently got lots of attention because Ghost uses it.  I haven't been able to find an exact reference to Shipit in Ghost's source, so it's presumably used for deploying their commercial hosted solution.  However, I actually thought Shipit might be useful as part of Ghost's open source stack, because it would help support people who download Ghost and deploy it to their own servers.  It would be interesting to discover more about the Ghost connection.
