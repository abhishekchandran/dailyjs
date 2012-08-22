---
layout: post
title: "Node Roundup: 0.8.7, Buffet, HARedis, Deployd"
author: "Alex Young"
categories: 
- node
- modules
- frameworks
- WebSocket
- redis
- libraries
---

<div class="intro">
You can send in your Node projects for review through our <a href="/contact.html">contact form</a> or <a href="http://twitter.com/dailyjs">@dailyjs</a>.
</div>

###Node 0.8.7

[Node 0.8.7](http://blog.nodejs.org/2012/08/15/node-v0-8-7-stable/) is out, which includes fixes for SSL, TLS, buffer and crypto issues, and also a few Windows-specific problems.  I noticed someone posted about an [issue with the latest npm in Windows](https://groups.google.com/d/topic/nodejs/2YWgVLBi1AE/discussion), but other than that 0.8.7 seems solid.

###Buffet

[Buffet](https://github.com/carlos8f/node-buffet) (License: _MIT_, npm: [buffet](https://npmjs.org/package/buffet)) by Carlos Rodriguez is a "performance-oriented" static file server:

> Buffet takes a fully-bufferred approach -- all files are fully loaded into memory when your app boots, so you will never feel the burn of the filesystem. In practice, this is immensely efficient. So much so that putting Varnish in front of your app might even make it slower!

It supports gzip, and will update files when they're changed.  The name of the `index.html` and `404.html` files can be changed, and other configuration options include `maxAge` for setting the `Cache-Control` header.

The author has included Mocha tests and the project is on [Travis CI](http://travis-ci.org/#!/carlos8f/node-buffet).

###HARedis

[HARedis](https://github.com/carlos8f/haredis) (License: _MIT_, npm: [haredis](https://npmjs.org/package/haredis)) also by Carlos Rodriguez is a wrapper around [node\_redis](https://github.com/mranney/node_redis) that helps build fault-tolerant clusters of Redis servers.  The main API difference is `createClient`, which accepts an array of hosts and ports, and this works with colon-separated strings for `'ip:port'`.

Carlos has included the test suite from the original redis module, so running `make test-cluster` or `make test` can be used to test the project.

###Deployd

[Deployd](http://deployd.com/) (GitHub: [deployd / deployd](https://github.com/deployd/deployd), License: _Apache 2.0_, npm: [deployd](https://npmjs.org/package/deployd)) by Ritchie Martori and the [Deployd team](https://github.com/deployd) is a toolkit for building real-time APIs suited to web and mobile applications.

Deployd applications are created with a command-line tool called `dpd`.  A newly created app includes a web IDE for managing the applications resources -- this is basically a schema that Deployd will use to generate a suitable RESTful API.  There's a [Deployd Hello World tutorial](http://www.deployd.com/docs/tutorials/hello-world.html) that covers the basics, and a [Deployd screencast](http://www.deployd.com/video.html).

The project is built on technologies like Socket.IO and MongoDB, and includes tests written with Mocha.
