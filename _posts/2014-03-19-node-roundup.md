---
layout: post
title: "Node Roundup: cipherhub, slate, express-di"
author: Alex Young
categories:
- node
- npm
- modules
---

###cipherhub

![Cipherhub](/images/posts/cipherhub.png)

Cipherhub (GitHub: [substack / cipherhub](https://github.com/substack/cipherhub), License: _MIT_, npm: [cipherhub](https://www.npmjs.org/package/cipherhub)) by substack is a module for encrypting messages based on GitHub public keys.

The usage is simple: `npm install -g cipherhub` and then `cipherhub USERNAME {OPTIONS} < message.txt`.

If there are multiple keys for the user, then you'll need to add a specific key with `cipherhub --add USERNAME < id_rsa.pub`.

###slate

![Slate](/images/posts/slate.png)

[Slate](https://github.com/slate/slate) is a new IRC client by TJ Holowaychuk that uses [node-webkit](https://github.com/rogerwang/node-webkit).  It's a native client in a similar spirit to [GitHub's Atom](https://atom.io/).

TJ notes that the project started as a small hack that he intended to expand into a Kickstarter project, but he's released it as an open source project instead.

> Conceptually I really just wanted a clean, minimalistic IRC client, completely extensible through plugins. Ideally most of the core is written using such plugins. The entire thing should be themable, and the default theme should be programmer-friendly, aka get all the clutter out of my way, I just want to see chat logs.

I'm making a collection of Node-powered native apps, so send those in if you're working on them.

###express-di

If you've got addicted to dependency injection through AngularJS, then you might be interested in [Express-di](http://luin.github.io/express-di/) (GitHub: [luin / express-di](https://github.com/luin/express-di), License: _MIT_, npm: [express-di](https://www.npmjs.org/package/express-di)) by Zihua Li:

{% highlight javascript %}
var express = require('express');
// Require express-di
require('express-di');
var app = express();

app.factory('people1', function(req, res, next) {
  next(null, { name: "Bob" });
});

app.factory('people2', function(req, res, next) {
  next(null, { name: "Jeff" });
});

app.get('/', function(people1, people2, res) {
  res.json({
    people1: people1,
    people2: people2
  });
});

require('http').createServer(app).listen(3008);
{% endhighlight %}

The `app.factory` method is used to define a dependency, and `req`, `res`, and `next` are handled as default dependencies.
