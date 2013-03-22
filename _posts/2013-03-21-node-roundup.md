---
layout: post
title: "Node Roundup: 0.10.1, Express Group Handlers, Fox, iWebPP.io"
author: "Alex Young"
categories: 
- node
- modules
- express
- middleware
- testing
- p2p
---

<div class="intro">
You can send in your Node projects for review through our <a href="/contact.html">contact form</a>.
</div>

###Node 0.10.1

[Node 0.10.1](http://blog.nodejs.org/2013/03/21/node-v0-10-1-stable/) has been released, hot on the heels of 0.10.0.  This version improves the performance of the non-streaming `crypto` APIs, fixes some `tls` and `net` module issues, and makes missing callbacks in _streams2_ show a warning rather than raising an exception.

###Express Group Handlers

Express Group Handlers (GitHub: [tldrio / express-group-handlers](https://github.com/tldrio/express-group-handlers), License: _MIT_, npm: [express-group-handlers](https://npmjs.org/package/express-group-handlers)) by Louis Chatriot provides a little bit of sugar for managing Express middleware.  It allows routes to be wrapped with `beforeEach` and `afterEach` so middleware can be confined to certain routes.

The `beforeEach` method can accept multiple middlewares to run, and it's easy to wrap it around existing code:

{% highlight javascript %}
var groupHandlers = require('express-group-handlers');

groupHandlers.setup(app);

app.beforeEach(groupHandler, function(app) {
  app.get('/route3', finalHandler3); // GET /route3 will execute groupHandler, then finalHandler3
});
{% endhighlight %}

###Fox

Fox (GitHub: [azer / fox](https://github.com/azer/fox), License: _BSD_, npm: [fox](https://npmjs.org/package/fox)) by Azer Koçulu is a test framework that is largely compatible with [Mocha](http://visionmedia.github.com/mocha/), as long as you don't have nested invocations of `describe`.  It works with both Node and client-side projects, and injects [chai](https://npmjs.org/package/chai) so you automatically get assertions without having to load an extra library.

Passing the `-b` flag to the command-line program will cause Fox to compile the scripts necessary to run the tests in a browser.  It also includes tests written with itself, of course!

###iWebPP.io

iWebPP.io (GitHub: [InstantWebP2P / iwebpp.io](https://github.com/InstantWebP2P/iwebpp.io), License: _MIT_, npm: [iwebpp.io](https://npmjs.org/package/iwebpp.io)) by Tom Zhou is a set of projects designed to send HTTP over UDP, the goal being to take advantage of UDP's inherent performance benefits.  It supports [TURN](http://en.wikipedia.org/wiki/Traversal_Using_Relay_NAT) and [STUN](http://en.wikipedia.org/wiki/STUN) channeling with WebSockets, for realtime streaming.

It can run web services using peer-to-peer protocols, behind NAT and firewalls.  The `iwebpp.io` module includes a binary called [node-httpp](https://github.com/InstantWebP2P/node-httpp), which provides the HTTP over UDP handling.  The project includes installation instructions, and a brief roadmap.

I've seen a few peer-to-peer Node projects, but I think this is the first one I've seen that uses UDP as the transport layer protocol.  It's also interesting that the author is directly addressing NAT issues.
