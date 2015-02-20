---
layout: post
title: "Fltspc, Mustache-Wax"
image: "/images/posts/mustache-wax.png"
author: Alex Young
categories:
- templating
- angularjs
- apps
- ui
---

###Fltspc

Clint Heyer from the IT University of Copenhagen sent in [Fltspc](http://fltspc.itu.dk/about), which is a collaborative whiteboard.  If you do group meetings where you want to work on snippets of text in a way that Google Docs doesn't quite cope with, then you might like to try this project out.

It can be extended with JavaScript and a REST API -- there's a GitHub repository with more information at [ClintH/fltspc-client](https://github.com/ClintH/fltspc-client), and I also found an [Android example](https://github.com/ClintH/fltspc-android).

Clint also shared a project they use to get students started with modern JavaScript development.  It's called [Kattegat](https://github.com/clinth/kattegat/), and it uses Yeoman and Express to get a server running with fun things like Socket.IO and Tessel.

If you're interested in Clint's Android work, then also take a look at Anders Bech Mellson's [Kiosker](https://github.com/mofus/kiosker/) project.  This is a generator for Android kiosk applications that displays a single web page, and it's configurable through JSON.  It sounds like this is what the students have been using to demo their interactive experiments on tablets.

###Mustache-Wax

![Mustache-Wax](/images/posts/mustache-wax.png)

[Mustache-Wax](http://jvitela.github.io/mustache-wax/) (GitHub: [jvitela/mustache-wax](https://github.com/jvitela/mustache-wax), License: _MIT_) by Jonathan Vitela is an extension for Mustache.js which allows you to use formatters inside expressions, in a style inspired by AngularJS.  By defining a list of methods on `Mustache.Formatters`, you'll be able to pass values through the filters.

The expressions use pipes, and you can chain them like this: `ten | add : 3.14159 | add : twenty | add:-3`.  The expression syntax supports arguments, which are denoted with `:`.

The documentation is nicely presented, and the project is well-tested.
