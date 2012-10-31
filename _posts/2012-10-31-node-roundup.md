---
layout: post
title: "Node Roundup: 0.8.14 and 0.9.3, Orange Mocha Frappuccino, WebSocketIPC"
author: "Alex Young"
categories: 
- node
- modules
- websockets
- testing
- mocha
---

<div class="intro">
You can send in your Node projects for review through our <a href="/contact.html">contact form</a> or <a href="http://twitter.com/dailyjs">@dailyjs</a>.
</div>

###0.8.14 and 0.9.3

Last week, [0.8.14](http://blog.nodejs.org/2012/10/25/node-v0.8.14/) and [0.9.3](http://blog.nodejs.org/2012/10/24/node-v0.9.3/) were released.  The 0.8.14 release is basically the 0.8.13 release with a fix for `EventEmitter`:

> Note: v0.8.13 contains a regression in the EventEmitter class. This is a bugfix release, but contains no new features. Most of the release notes are copied from v0.8.13, since it didn't live long.

The 0.9 release updates V8 and has various bug fixes.  It also adds an `options` argument to [util.inspect](http://nodejs.org/docs/v0.9.3/api/all.html#all_util_inspect_object_options) -- the older API had three arguments, so reducing the arity makes sense as new options can be supported more easily.

###Orange Mocha Frappuccino

[Orange Mocha Frappuccino](https://github.com/brianc/node-omf) (License: _MIT_, npm: [omf](https://npmjs.org/package/omf)) by Brian Carlson is a library to help build HTTP verification tests with [Mocha](http://visionmedia.github.com/mocha/).  It can accept a Node HTTP server or URLs:

{% highlight javascript %}
var omf = require('omf');
var assert = require('assert');

omf('https://github.com', function(client) {
  client.get('/brianc/node-omf', function(response){
    response.has.statusCode(200);
    response.has.body('ORANGE MOCHA FRAPPUCCINO');

    //the full response is available to any custom tests:
    it('has ETag header', function() {
      assert(this.response.headers['etag']).ok();
    });
  });
});
{% endhighlight %}

This is a little bit more like how Cappuccino worked, which was TJ's pre-Mocha test framework.

###Crawlme

[Crawlme](https://github.com/OptimalBits/Crawlme) (License: _MIT_, npm: [crawlme](https://npmjs.org/package/crawlme)) from Optimal Bits is Connect middleware for automatically mapping hashbang URLs to parameter-based URLs for [Googlebot Ajax Crawling](https://developers.google.com/webmasters/ajax-crawling/docs/getting-started).

###WebSocketIPC

[WebSocketIPC](https://github.com/nfroidure/WebSockIPC) (License: _GPL_) by Nicolas Froidure is a proof-of-concept of his [VarStream](https://github.com/nfroidure/VarStream) "variable exchange format".  This format is designed to be human readable, streamable, and self-referencial.

WebSocketIPC uses WebSockets to synchronise a variable tree between multiple clients and a server.  It can also synchronise data between multiple Node instances by piping VarStreams.

It's interesting that as interest in using streams grows more diverse projects are appearing to better exploit their properties.
