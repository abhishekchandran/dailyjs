---
layout: post
title: "Node Roundup: Express 3.0, Declare, Sourcery"
author: "Alex Young"
categories: 
- node
- modules
- http
- frameworks
- express
- object-oriented
---

<div class="intro">
You can send in your Node projects for review through our <a href="/contact.html">contact form</a> or <a href="http://twitter.com/dailyjs">@dailyjs</a>.
</div>

###Express 3.0

[Express 3.0](http://expressjs.com/) (GitHub: [visionmedia / express](https://github.com/visionmedia/express), License: _MIT_, npm: [express](https://npmjs.org/package/express)) has been released, announced by TJ in a [blog post with more details](http://tjholowaychuk.com/post/34189797102/express-3-0) on Express 3.0 and Connect 2.

There's a [2.x to 3.x migration guide](https://github.com/visionmedia/express/wiki/Migrating-from-2.x-to-3.x) and a [list of Express 3.x features](https://github.com/visionmedia/express/wiki/New-features-in-3.x).  In particular, `express()` now returns a `Function` that can be used with Node's `http.createServer`, you'll need to update the way helpers work, and there are a few changes to the request and response objects.

The Express website now also includes a list of [applications powered by Express](http://expressjs.com/applications.html), which is useful for those of us evaluating frameworks for use in a new project.

###Declare

[Declare](http://doug-martin.github.com/declare.js/) (GitHub: [doug-martin / declare.js](https://github.com/doug-martin/declare.js), License: _MIT_, npm: [declare.js](https://npmjs.org/package/declare.js)) by Doug Martin is an attempt to help write object oriented code that runs on both the client and server.  The resulting classes can be used with [RequireJS](http://requirejs.org/), and support features like mixins, super methods, static methods, and getters and setters.

The author has included some simple tests, and detailed usage examples.

###Sourcery

[Sourcery](https://github.com/vesln/sourcery) (License: _MIT_, npm: [sourcery](https://npmjs.org/package/sourcery)) by Veselin Todorov is designed for creating RESTful API clients.  It's influenced by [ActiveResource](https://github.com/rails/activeresoucre), so it should work well with many CRUD-oriented REST APIs.  It supports basic authentication as well:

{% highlight javascript %}
var BasicAuth = require('sourcery').BasicAuth;

var Base = Resource.extend({
  host: 'http://example.com/api/v1'
, auth: {
    type:  BasicAuth
  , user: 'replace-with-real-user'
  , pass: 'replace-with-real-pass'
  }
});
{% endhighlight %}

It includes Mocha tests, and is built using the popular [request HTTP client library](https://npmjs.org/package/request) by Mikeal Rogers.
