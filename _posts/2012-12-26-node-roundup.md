---
layout: post
title: "Node Roundup: 0.9.4, screener, Jyql"
author: "Alex Young"
categories: 
- node
- modules
---

<div class="intro">
You can send in your Node projects for review through our <a href="/contact.html">contact form</a> or <a href="http://twitter.com/dailyjs">@dailyjs</a>.
</div>

###Node 0.9.4

[Node 0.9.4](http://blog.nodejs.org/2012/12/21/node-v0-9-4-unstable/) has been released, and this version is a milestone because it features the [new streams API](http://blog.nodejs.org/2012/12/20/streams2/).  There are the usual platform-specific bug fixes and other improvements to core modules.

The [new streams API documentation](http://nodejs.org/docs/v0.9.4/api/stream.html) was published as part of this release.

###node-screener

[node-screener](https://github.com/RushPL/node-screener/) (License: _BSD_, npm: [screener](https://npmjs.org/package/screener)) by Damian Kaczmarek is a module for validating objects, and the author notes it works with Mongoose:

{% highlight javascript %}
var screen = require('screener').screen;
var object = {
  _id: "503cb6d92c32a8cd06006c53",
  user: { name: "Joe Doe", birthdate: "04.07.1980"},
  location: { lat: 16.5015636, lon: 52.1971881 }
};

var result = screen(object, {
  user: {
    name: 'string', // same effect would be if passed /.*/ regexp
    birthdate: /\d\d\.\d\d\.\d\d\d\d/
  }
  location: {lat: 'number', lon: 'number'}
});
{% endhighlight %}

###Jyql

[Jyql](https://github.com/giacecco/jyql) (License: _MIT_, npm: [jyql](https://npmjs.org/package/jyql)) by Gianfranco Cecconi is a Node module and browser library for working with the Yahoo! Query Language engine.  The Node module uses the [request](https://npmjs.org/package/request) module by Mikeal Rogers to automatically fetch a suitable resource to be processed with YQL.

