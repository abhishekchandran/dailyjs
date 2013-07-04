---
layout: post
title: "Node Roundup: 0.11.3, Busboy, connect-mongostore, Chance"
author: "Alex Young"
categories: 
- node
- modules
- html
- forms
- middleware
- testing
- sessions
- connect
---

<div class="intro">
You can send in your Node projects for review through our <a href="/contact.html">contact form</a>.
</div>

###Node 0.11.3

[Node 0.11.3](http://blog.nodejs.org/2013/06/26/node-v0-11-3-unstable/) was released last week, which was a fairly large update: libuv, [c-ares](http://c-ares.haxx.se/), and v8 were all updated.  The debugger now breaks on uncaught exceptions, and there were changes to enable dtrace for libuv's probes (if enabled).  The underlying implementation for buffers has undergone major changes as well -- I've picked out a few commits here that discuss the updates:

* [buffer: reimplement Buffer pools](https://github.com/joyent/node/commit/456942a920fe313ebe0b0da366d26ef400ec177e)
* [buffer: use smalloc as backing data store](https://github.com/joyent/node/commit/3a2f273bd73bc94a6e93f342d629106a9f022f2d)

It looks like these changes should make the buffer implementation more robust.  I've checked out Node 0.11.x and 0.10.x on my local machine and run `make bench-buffer` against both, so far 0.11 doesn't look conclusively faster, but I haven't been particularly scientific about the process yet.

###Busboy

Busboy (GitHub: [mscdex / busboy](https://github.com/mscdex/busboy), License: _MIT_, npm: [busboy](https://npmjs.org/package/busboy)) by Brian White is a streaming HTML form data parser.  It uses the [Dicer](https://npmjs.org/package/dicer) module to parse multipart fields, and also uses a stream parser for urlencoded fields.

The busboy API allows limits to be placed on the incoming data.  The `Busboy` constructor accepts an `options` object which may include a `limits` property.  Limits can include `fieldNameSize`, `fieldSize`, `files`, and more -- see the readme for full documentation.  These options mostly default to `Infinity`, apart from `fieldNameSize` which is 100 bytes.

Tests are included, and it should be possible to use it as Express middleware fairly easily.

###connect-mongostore

How do you decide which session middleware to use?  Use cookies during early development then quickly search npm for something that uses your database?  Me too!  But there are better options out there and it's worth taking a bit of time to research them.  Ilya Shaisultanov sent in connect-mongostore (GitHub: [diversario / connect-mongostore](https://github.com/diversario/connect-mongostore/), License: _MIT_) whichi is an attempt to write a cleaner session store that takes advantages of features like replica sets, and has test coverage.

###Chance

![Chance](/images/posts/chance.png)

[Chance](http://chancejs.com/) (GitHub: [victorquinn / chancejs](https://github.com/victorquinn/chancejs), License: _MIT_, npm: [chance](https://npmjs.org/package/chance)) by Victor Quinn is a library for generating random stings, numbers, and even things that are useful for test data like address elements and names.

It works in browsers and Node, and has a simple constructor-based API:

{% highlight javascript %}
var Chance = require('chance');
var chance = new Chance();
chance.name({ middle: true });
{% endhighlight %}
