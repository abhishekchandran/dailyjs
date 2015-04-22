---
layout: post
title: "Node Roundup: io.js 1.8.1, ioredis, fetchival"
author: Alex Young
categories:
- node
- iojs
- modules
- libraries
- npm
- http
- rest
- redis
---

###io.js 1.8.1

[io.js](https://iojs.org/) 1.8.1 has been released.  As always the [changelog](https://github.com/iojs/io.js/blob/v1.x/CHANGELOG.md) is concise and informative.  You might want to update to this release if you use npm's new scoped modules -- there's a fix for scoped packages with `peerDependencies`.

###npm Private Modules and Heroku

I've started moving my old private modules that I deployed using GitHub and OAuth tokens to [npm Private Modules](https://www.npmjs.com/private-modules), and so far it's worked well.  To make this work with Heroku I still had to set a token for Heroku to be able to access my modules through npm -- I found a post that explains how to do this here: [npm Private Modules with Heroku](http://blog.getpiggybank.com/npm-private-modules-with-heroku/).

###ioredis

ioredis (GitHub: [luin/ioredis](https://github.com/luin/ioredis), License: _MIT_, npm: [ioredis](https://www.npmjs.com/package/ioredis)) is a Redis client used by [Alibaba](http://en.wikipedia.org/wiki/Alibaba_Group).  It works with Node callbacks (`err, result`) and promises.

The authors describe it as more robust than the [redis](https://www.npmjs.com/package/redis) package, and the benchmarks show that it's faster as well.  It supports binary data, and ES6 types like `Map` and `Set`.  It also has several other advantages over the `node_redis` module, so you should definitely test it out if you depend on Redis.

###fetchival

Typicode sent in fetchival (GitHub: [typicode/fetchival](https://github.com/typicode/fetchival), License: _MIT_, npm: [fetchival](https://www.npmjs.com/package/fetchival)), a module for making [fetch](https://github.com/github/fetch) requests with JSON.  Fetch is a function for making web requests with promises, based on the [Fetch spec](https://fetch.spec.whatwg.org).  Fetchival makes posts a lot easier to read:

{% highlight javascript %}
fetchival('/users').post({
  name: 'Typicode',
  login: 'typicode'
})
.then(function(json) {
  // ...
})
{% endhighlight %}

Naturally this works in Node, but it should also work in browsers as well, which makes it a very clean alternative to other `XMLHttpRequest` wrappers.
