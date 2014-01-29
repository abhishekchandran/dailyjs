---
layout: post
title: "jQuery 1.11 and 2.1, Backbone.global"
author: Alex Young
categories:
- jquery
- backbone
---

###jQuery 1.11 and 2.1 Released

[jQuery 1.11 and 2.1 have been released](http://blog.jquery.com/2014/01/24/jquery-1-11-and-2-1-released/):

> both the 1.x and 2.x branches of jQuery support all recent modern browsers and have the same API. The 1.x branch, this time 1.11.0, adds support for the older versions of Internet Explorer (IE6, 7, and 8). The 2.x branch, today played by 2.1.0, adds support for non-traditional web environments like node.js and browser plugins for Chrome and Firefox.

Another interesting point from the release notes was this paragraph about source map problems:

> This release does not contain the sourcemap comment in the minified file. Sourcemaps have proven to be a very problematic and puzzling thing to developers, spawning hundreds of confused developers on forums like StackOverflow and causing some to think jQuery itself was broken.

I've noticed source maps confuse CoffeeScript developers as well, so this isn't surprising.  The tools seem solid -- [Chrome's implementation has worked for me in the past](https://developers.google.com/chrome-developer-tools/docs/javascript-debugging#source-maps), but the concept itself isn't entirely intuitive.

The Node/browserify support is handy -- that particular change was [ticket 14677](http://bugs.jquery.com/ticket/14677).

###Backbone.global

Backbone.global (GitHub: [DarrylD / Backbone.global](https://github.com/DarrylD/Backbone.global), License: _MIT_) allows you to listen to global events in a Backbone.js application.  It changes `Backbone.View.prototype.delegateEvents` to emit events on a global event bus, which makes it easier to hook into events for things like testing or logging.
