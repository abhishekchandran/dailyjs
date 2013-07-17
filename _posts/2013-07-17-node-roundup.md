---
layout: post
title: "Node Roundup: 0.11.4, NodeICO, Node-FSAPI"
author: "Alex Young"
categories: 
- node
- modules
- http
- restify
- services
---

<div class="intro">
You can send in your Node projects for review through our <a href="/contact.html">contact form</a>.
</div>

###Node 0.11.4

[Node 0.11.4](http://blog.nodejs.org/2013/07/12/node-v0-11-4-unstable/) was released last week.  The major dependencies have been upgraded (npm, v8, c-ares), and there's a change in behaviour for timers: `setImmediate` has been changed to [process the full queue on each turn](https://github.com/joyent/node/issues/5798).

There are also other tweaks and improvements for HTTP, buffer, stream, crypto, and zlib.  The brief fluffy of work on HTTP involved [new Agent code](https://github.com/joyent/node/commit/40e92650bb97b736b8e29c5de35c1c29ebd625ef) and [fixed keepAlive behaviour](https://github.com/joyent/node/commit/9fc9b87472806147b83c24d85b303c4f75d3021c).

###NodeICO

[NodeICO](https://nodei.co/) (GitHub: [rvagg / nodei.co](https://github.com/rvagg/nodei.co), License: _MIT +no-false-attribs_) is an open source service that displays badges for Node modules.  As an example, this is what the Express badge looks like:

<img src="https://nodei.co/npm/express.png" alt="" style="border: none" />

There's also a cool graph version:

<img src="https://nodei.co/npm-dl/express.png?months=9" alt="" style="border: none" />

The project was written by Rod Vagg and uses restify.

###Node-FSAPI

Speaking of restify, Kent Safranski sent in Node-FSAPI (GitHub: [Fluidbyte / Node-FSAPI](https://github.com/Fluidbyte/Node-FSAPI)), which is a project to provide a RESTful server for interacting with remote file systems.  It supports three layers of security: URL keys, IP restriction, and HTTPS.

The client implementation supports Ajax, so [from what I can tell](https://github.com/Fluidbyte/Node-FSAPI/blob/master/client.js#L178) you could use it as a browser-based solution for storing files.
