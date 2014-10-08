---
layout: post
title: "Node Roundup: Nightmare, Prototypes, node-libpq and node-pg-native"
author: "Alex Young"
image: "/images/posts/nightmare.png"
categories:
- modules
- libraries
- node
- npm
- phantom
- postgres
---

###Nightmare

![Nightmare](/images/posts/nightmare.png)

By far the most brittle and confusing part of testing is full stack integration testing.  I've used lots of different approaches, whether they're based on PhantomJS or Selenium, but they always cause me trouble.

One issue is often the API -- PhantomJS itself has a strange API if you're more used to Node development.  That's why I was excited to hear about [Nightmare](http://www.nightmarejs.org/) (GitHub: [segmentio / nightmare](https://github.com/segmentio/nightmare), License: _MIT_, npm: [nightmare](https://www.npmjs.org/package/nightmare)), which aims to simplify Phantom's API.

If you want to try it out be aware that you'll need to install PhantomJS on your system.  This can be done using Homebrew on a Mac, and there are [packages for other platforms on the main site](http://phantomjs.org/).

Nightmare has a chainable API that allows you to evaluate JavaScript on the target page's DOM.  If you've got a page with jQuery on it, for example, then you can access `$` in the `evaluate` callback.

Here I've loaded a web app that starts a server (in `app.js`), then filled out a sign in form and submitted it.  The code in the `evaluate` method will be executed on the page, so I can use jQuery to do DOM stuff.

{% highlight javascript %}
var server = require('./app');
var Nightmare = require('nightmare');
new Nightmare()
  .goto('http://localhost:3000')
  .type('input[name="email"]', 'alex@example.com')
  .type('input[name="password"]', 'password')
  .click('.sign-in')
  .evaluate(function() {
    return $('.sign-out').is(':visible');
  }, function(visible) {
    assert(visible, '.sign-out should be visible');
  })
  .run(function() {
    server.close();
  });
{% endhighlight %}

Naturally you can use this for the general chores you'd use Phantom for, but I think it might be quite cool for testing projects with complex client-side code.

###Prototypes

Alex Fernández sent in prototypes (GitHub: [alexfernandez / prototypes](https://github.com/alexfernandez/prototypes), License: _MIT_, npm: [prototypes](https://www.npmjs.org/package/prototypes)).  This module modifies prototype objects, so use it with caution, but you might find some of the methods useful.

Here are some examples:

{% highlight javascript %}
'pepitus'.startsWith('pep');
'hi.there'.substringFrom('.'); // 'there'

{ a: 1, b: 2 }.forEach(function(value, key) {
  console.log(key, value);
});
{% endhighlight %}

###node-libpq and node-pg-native

node-libpq (GitHub: [brianc / node-libpq](https://github.com/brianc/node-libpq), License: _MIT_, npm: [libpq](https://www.npmjs.org/package/libpq)) by Brian M. Carlson is a set of native bindings to the PostgreSQL libpq C client library.

> This module attempts to mirror as closely as possible the C API provided by libpq and provides the absolute minimum level of abstraction. It is intended to be extremely low level and allow you the same access as you would have to libpq directly from C, except in node.js! The obvious trade-off for being "close to the metal" is having to use a very "c style" API in JavaScript.

Brian is the author of the popular [pg](https://github.com/brianc/node-postgres) PostgreSQL library, and has also recently released [node-pg-native](https://github.com/brianc/node-pg-native).  node-pg-native is a high performance PostgreSQL module that uses node-libpq.

Sean Levy sent in node-pg-native because he's excited about the synchronous API:

{% highlight javascript %}
var rows = client.querySync('SELECT NOW() AS the_date')
console.log(rows[0].the_date) //Tue Sep 16 2014 23:42:39 GMT-0400 (EDT)
{% endhighlight %}

It's really that simple!
