---
layout: post
title: "Node Roundup: 0.10.31, One-Shot Budapest, Tenso"
author: "Alex Young"
categories:
- modules
- libraries
- npm
- node
- events
---

###0.10.31

Node has been updated to [0.10.31](http://blog.nodejs.org/2014/08/19/node-v0-10-31-stable/), which includes a newer version of v8, openssl, npm, and bug fixes for some core modules.  This includes a fix for `fs` where `fs.readFileSync` could leak file descriptors, and a fix for `Readable.wrap`'s handling of `objectMode` falsy values.

* [cluster: disconnect should not be synchronous](https://github.com/joyent/node/commit/2fd7ee12d9ee02cc310bd1126a9f09a6a7abe630#diff-d41d8cd98f00b204e9800998ecf8427e)
* [fs: fix fs.readFileSync fd leak when get RangeError](https://github.com/joyent/node/commit/cc08106d6283040fc4c58005b639dae366b18b67#diff-d41d8cd98f00b204e9800998ecf8427e)
* [stream: fix Readable.wrap objectMode falsy values](https://github.com/joyent/node/commit/8e2cc69e7883b0a8d97a2f62e301ece209f61352)
* [timers: fix timers with non-integer delay hanging](https://github.com/joyent/node/commit/6f043940bdcbfb5272be8ae959cd74b9fb5cf4f8#diff-d41d8cd98f00b204e9800998ecf8427e)

###One-Shot Budapest

The [NodeConf One-Shot: Budapest](http://oneshot.risingstack.com/) conference will be held on November 21th, 2014.  Tickets are $100, and talks include:

* Matteo Collina: Hardware Hacking on Stage
* Mathias Buus: BitTorrent, p2p with Node.js
* Julian Gruber: Node.js vs Go
* Nuno Job: Production Ready Node

###Tenso

[Tenso](http://avoidwork.github.io/tenso/examples.html) (GitHub: [avoidwork/tenso](https://github.com/avoidwork/tenso), License: _BSD-3_, npm: [tenso](https://www.npmjs.org/package/tenso)) by Jason Mulligan is a REST API facade.  It supports caching, DTrace, and decorates response/request objects in a similar way to Express/restify.

{% highlight javascript %}
var uuid = require( 'keigai' ).util.uuid;

module.exports.get = {
  '/': [],

  '/reports/tps': function(req, res) {
    res.error(new Error('TPS Cover Sheet not attached'), 785);
  },

  '/uuid': function(req, res) {
    res.respond(uuid(), 200, {'cache-control': 'no-cache'});
  }
};
{% endhighlight %}

