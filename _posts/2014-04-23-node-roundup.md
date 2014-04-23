---
layout: post
title: "Node Roundup: npm-pkgr, Promised Land, Stash.js"
author: "Alex Young"
categories:
- node
- modules
- npm
- caching
---

###npm-pkgr

npm-pkgr (GitHub: [vvo / npm-pkgr](https://github.com/vvo/npm-pkgr), License: _ISC_, npm: [npm-pkgr](https://www.npmjs.org/package/npm-pkgr)) by Vincent Voyer caches `npm install` results based on your `package.json` and `npm-shrinkwrap.json` files.

Depending on your set up, this should reduce the time taken to deploy Node projects.  The basic usage is `npm-pkgr` instead of `npm install`, and `npm-pkgr --production` to use `npm-shrinkwrap.json`.

###Promised Land

Promised Land (GitHub: [FredyC / promised-land](https://github.com/FredyC/promised-land/), License: _MIT_, npm: [promised-land](https://www.npmjs.org/package/promised-land)) provides a way of wrapping modules with an `EventEmitter` that allows you to use promises across your application.

For example, let's say you've got a module that connects to a database.  Once the connection is ready, it does this:

{% highlight javascript %}
var Land = require('promised-land');
Land.emit('database:connected', db);
{% endhighlight %}

Any other module that needs to know when the database is ready can now do so with promises:

{% highlight javascript %}
var Land = require('promised-land');
Land.promise('database:connected').then(function(db) {
  doSomethingWithDatabase();
});
{% endhighlight %}

It also allows events to be repeated, in a stream-like way:

{% highlight javascript %}
Land.stream('database:row').onValue(function(val) {
  doSomethingRepeatedly();
});
{% endhighlight %}

The project has tests and more examples in the readme.

###Stash.js

Stash.js (GitHub: [tadeuzagallo / stash.js](https://github.com/tadeuzagallo/stash.js), License: _MIT_, npm: [stash.js](https://www.npmjs.org/package/stash.js)) by Tadeu Zagallo is a multilayer cache manager.  That means you can define and use different storage systems for caching, based on "drivers".

So far the author has added a driver for ephemeral storage and `localStorage` support for browsers.

Cache items have methods for determining cache miss, locking, and setting values:

{% highlight javascript %}
var stash = new Stash.Pool();
var item = stash.getItem('my/key/path');
var data = item.get();

if (item.isMiss()) {
  item.lock();
  data = 'example';
  item.set(data, cacheDuration);
}
{% endhighlight %}

What `lock` does here is dependent on the cache policy.  There are four policies that are explained in the readme.
