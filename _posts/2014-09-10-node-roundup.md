---
layout: post
title: "Node Roundup: promise.io, copromise, Apper"
author: "Alex Young"
categories:
- modules
- node
- libraries
- express
- frameworks
- promises
- async
---

###promise.io

promise.io (GitHub: [krillr / promise.io](https://github.com/krillr/promise.io), License: _Apache 2.0_, npm: [promise.io](https://www.npmjs.org/package/promise.io)) by Aaron Krill is an RPC module that uses promises.  You can create a server like this:

{% highlight javascript %}
var server = new PromiseIO({
  someFunc: function(input) {
    return 'I got: ' + input;
  }
});

server.listen(3000);
{% endhighlight %}

Then the client can call `someFunc` by connecting to the server:

{% highlight javascript %}
var client = new PromiseIO();

client.connect('http://localhost:3000').then(function(remote) {
  return remote.someFunc('my variable!');
}).then(function(returnVal) {
  return console.log(returnVal);
}).catch(function(err) {
  return console.log(err);
});
{% endhighlight %}

Internally, [q](https://www.npmjs.org/package/q) is used for the promise implementation.

###copromise

copromise (GitHub: [deanlandolt / copromise](https://github.com/deanlandolt/copromise), License: _MIT_, npm: [copromise](https://www.npmjs.org/package/copromise)) by Dean Landolt is a bit like [co](https://www.npmjs.org/package/co), but it automatically lifts values that aren't promises, so you can `yield` anything.

> A `copromise` represents the eventual value of a coroutine. A coroutine is a generator function where the `yield` keyword is used to suspend execution to wait on a future value, allowing linear control flow logic for asynchronous code.

Dean announced it [on the nodejs list](https://groups.google.com/d/topic/nodejs/u7xTQ5Tx-ts/discussion), including some examples and a comparison with the co module.

###Apper

[Apper](http://asyncanup.github.io/apper/) (GitHub: [asyncanup / apper](https://github.com/asyncanup/apper), License: _MIT_, npm: [apper](https://www.npmjs.org/package/apper)) by Anup Bishnoi is a real-time framework for single page applications.  The idea behind it is to have strong conventions for practices that suit single page apps, including transparent minification and bundling.

It wraps around Express, so route definitions look like a typical Express project, but Apper also has specific places for things like middleware and application settings.

If you're new to Express then you might like working with the conventions Apper uses, and it will at least push you away from putting everything in a monolithic `app.js` file.
