---
layout: post
title: "Node 0.10"
author: "Alex Young"
categories: 
- node
---

[Node 0.10 is about to be released](https://github.com/joyent/node/commit/163ca274230fce536afe76c64676c332693ad7c1) -- the next stable version of Node.  The most major change is the new streams API, which is designed to overcome some of the limitations found in previous versions.  For a summary of the issues with streams in Node 0.8 and the new API, see: [A New Streaming API for Node v0.10](http://blog.nodejs.org/2012/12/20/streams2/).

At first the new streams API seems quirky to work with, but I'm convinced my _streams2_ code is leaner.  There are also new base classes for streams: `Readable`, `Writable`, `Duplex`, and `Transform`.  These classes actually cover some key functionality that was previously provided by third party modules.

Many of Node's core modules have streaming interfaces, and 0.10 adds streaming APIs to the crypto module.

`EventEmitter` has some changes.  The documentation recommends using `util.inherits` to extend the `EventEmitter` class, and I'd add that it's a good idea to call the constructor as well.  There's also a new `removeListener` event which is emitted when listeners are removed, including when `removeAllListeners` is called.

<div class="image">
  <img src="/images/posts/setimmediate.png" alt="" />
  <small>setImmediate semantics in Node 0.9.x</small>
</div>

Node now has [setImmediate](https://developer.mozilla.org/en-US/docs/DOM/window.setImmediate) and `clearImmediate` -- there's a useful diagram by Shigeki Ohtsu that shows where `setImmediate` is triggered: [setImmediate semantics in Node 0.9.x](https://github.com/joyent/node/pull/3872#issuecomment-7804775).

For more details on API changes, see [Api changes between v0.8 and v0.10](https://github.com/joyent/node/wiki/Api-changes-between-v0.8-and-v0.10).
