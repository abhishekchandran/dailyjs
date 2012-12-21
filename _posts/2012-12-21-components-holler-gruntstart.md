---
layout: post
title: "New Streaming API for Node, Components Tutorial, Holler, GruntStart"
author: Alex Young
categories: 
- components
- grunt
- node
- streams
---

###New Streaming API for Node

In [New Streaming API for Node](http://blog.nodejs.org/2012/12/21/streams2/), Isaac Schlueter outlines the issues found in Node's current streaming API, and presents the new Node 0.10 API that addresses these problems.  Although the documentation makes it clear that the stream API is "unstable", it's notable for two reasons: it's built on `EventEmitter`, and many of Node's core modules have stream interfaces.  Streams are an integral part of Node, and it's becoming clear that many problems are best solved with streams.

The 0.10 version of streams will cause backward compatibility issues, but this has been considered and mitigated:

> For backwards compatibility with older Node programs, Readable streams switch into "old mode" when a `'data'` event handler is added, or when the `pause()` or `resume()` methods are called.

Isaac has included the new stream API's documentation in the post, and if you're working with Node at all it's worth reading.  If you're struggling to understand the motivation behind the changes, it boils down to `pause()` not really pausing, and the potential for `'data'` events to be dropped before they're ready to be consumed.  I liked Isaac's practical example of this issue:

> `'data'` events come right away (whether you're ready or not). This makes it unreasonably difficult to do common tasks like load a user's session before deciding how to handle their request.

So, read [A New Streaming API for Node v0.10](http://blog.nodejs.org/2012/12/21/streams2/) carefully even if you're not working with streams directly.  I'm of the opinion that you _should_ be thinking about streams when designing Node programs, and if Node's core developers can get them right for version 0.10 it'll be a huge win for the platform.


###Components Tutorial

![The date picker from the tutorial](/images/posts/picker2.png)

TJ Holowaychuk has written up a detailed tutorial on [Components](https://github.com/component), about [building a date picker](http://tjholowaychuk.com/post/37832588021/building-a-date-picker-component).  I'm a believer of the Components idea, and at the moment good tutorials are lacking in this area, so it's good to see TJ writing up detailed examples like this.

There are also some screencasts available: [Creating components](http://vimeo.com/53730178), and [Web Components - Introduction](http://vimeo.com/48054442).

###Holler.js

[Holler.js](http://bitpshr.info/holler/) (GitHub: [bitpshr / holler](https://github.com/bitpshr/holler), License: _WTFPL_, npm: [holler](https://npmjs.org/package/holler)) by Paul Bouchon is a real-time notification service.  It's distributed as a Node module with client-side code that builds on [alertifyjs](http://fabien-d.github.com/alertify.js/).

The real-time communication is handled by [Faye](http://faye.jcoglan.com/).  Paul has made a [brief demonstration video](http://vimeo.com/55747016) to show how it works.

###GruntStart

![GruntStart](/images/posts/gruntstart.png)

[GruntStart](http://tsvensen.github.com/GruntStart/) (GitHub: [tsvensen / GruntStart](https://github.com/tsvensen/gruntstart), License: _MIT, GPL_) by Tim Svensen is a Grunt task for building optimised websites using [HTML5 Boiler Plate](http://html5boilerplate.com/), jQuery, Modernizr and [Respond.js](https://github.com/scottjehl/Respond).  It includes a task that watches for file changes and automatically generates optimised assets.

The client-side scripts are all included, so all you need to do to get started is download GruntStart from GitHub.
