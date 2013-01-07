---
layout: post
title: "OOGL, Jot, Conference"
author: Alex Young
categories:
- webgl
- text
- editor
---

###OOGL

![oogle.js](/images/posts/ooglejs.png)

[OOGL](http://www.oogljs.com/) (GitHub: [71104 / oogl.js](https://github.com/71104/oogl.js), License: _MIT_) by Alberto La Rocca is a thin object-oriented library to make WebGL easier to work with.  It has asynchronous shader loading, texture and attribute array management, and a render loop implemented with `requestAnimationFrame` and a `setInterval` fallback.

The author has written an [API reference for oogl.js](http://71104.github.com/oogl.js/doc/), and there are some [oogle.js demos as well](http://71104.github.com/oogl.js/demos/).

###Jot

![Jot](/images/posts/jotwiki.png)

[Jot](http://jotwiki.boutell.com/) (GitHub: [boutell / jot](https://github.com/boutell/jot), License: _MIT_, npm: [node-jot](https://npmjs.org/package/node-jot)) by Tom Boutell is a text editor built with Express and some client-side libraries like [Rangy](http://code.google.com/p/rangy/), and has some options for MongoDB as well.

Media files like photos and videos are supported, using a _widgets_ system:

> Jot introduces "widgets," separate editors for rich media items like photos, videos, pullquotes and code samples. Jot's widgets handle these items much better than a rich text editor on its own.

Also, Jot can be configured to send uploaded files to Amazon S3 or a custom backend solution.  It uses ImageMagick to process image files.

It has the usual rich text editing features as well, and supports major browsers from IE7 up.

The author has provided instructions on how to integrate Jot with another Express application.

###Conference

[Conference](http://github.com/axemclion/conference) (GitHub: [axemclion / conference](https://github.com/axemclion/conference), License: _MIT/GPL_) by Parashuram Narasimhan is a Backbone.js application that provides an example schedule for a conference.  Designed to alleviate the symptoms of bad conference wi-fi, Conference stores the data about the conference locally to avoid requiring a data connection once it has been initially loaded.

I've seen conferences that use custom native mobile apps to do a similar thing, but this version would be suitable for a mobile browser as well (and free as it's released under a permissive license).  Anyway, it's an interesting use of Backbone.js, and Parashuram would like to help conferences adopt it.

