---
layout: post
title: "Node Roundup: npmE, Snapshot.js, dm.js"
author: "Alex Young"
categories:
- node
- modules
- libraries
- npm
- dependency-injection
---

###npmE

There's an [open beta for npmE](https://www.npmjs.org/enterprise#private), the npm Enterprise programme.  This allows you to sign in to a private, hosted repository, which can be used to distribute private modules.  They're prefixed with your company name, like this:

{% highlight text %}
npm install @myco/somepackage
{% endhighlight %}

Then you can load them with the prefix as follows:

{% highlight javascript %}
require('@myco/somepackage');
{% endhighlight %}

There's a new post on the npm blog about the [roadmap for npmE](http://blog.npmjs.org/post/93509138505/npm-enterprise-roadmap):

> We plan on building a web-UI for controlling various aspects of an npmE installation: adding and removing packages from the whitelist, configuring authentication/authorization strategies, managing organizations and teams.

###Snapshot.js

Snapshot.js (GitHub: [Wildhoney/Snapshot.js](https://github.com/Wildhoney/Snapshot.js), License: _MIT_, [Demo](http://node-snapshot.herokuapp.com/)) by Adam Timberlake is a WebSocket-based Node application for sorting, paginating, and filtering data served using WebSockets.

It uses Express and the [crossfilter](https://www.npmjs.org/package/crossfilter) module, which is a multidimensional filtering library:

> Crossfilter is a JavaScript library for exploring large multivariate datasets in the browser. Crossfilter supports extremely fast interaction with coordinated views, even with datasets containing a million or more records; we built it to power analytics for Square Register, allowing merchants to slice and dice their payment history fluidly.

###dm.js

dm.js (GitHub: [gobwas / dm.js](https://github.com/gobwas/dm.js), License: _MIT_, npm: [dm](https://www.npmjs.org/package/dm)) by Sergey Kamardin is a module for dependency injection.  It's service based, so you'd have to build applications using that pattern to take advantage of it.

The `dm` module itself implements the "service locator" pattern.  That means it knows how to find a given service and configure it.  It supports asynchronous adapters, so you could use it with jQuery.Deferred, Q.js, and promises with Harmony.  It can load modules with either AMD or CommonJS, so it'll work with Node modules.

This might sound like a huge amount of effort if you're not used to dependency injection, but if you come from a Java/C#/C++ background then you might find it easier to design Node applications this way.
