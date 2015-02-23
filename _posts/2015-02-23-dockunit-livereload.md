---
layout: post
title: "Dockunit, easy-livereload"
author: Alex Young
categories:
- testing
- docker
- express
- middleware
---

###Dockunit

Dockunit (GitHub: [tlovett1/dockunit](https://github.com/tlovett1/dockunit), License: _GPL_, npm: [dockunit](https://www.npmjs.com/package/dockunit)) by Taylor Lovett is a Node command-line tool for running tests in Docker containers.  You can define a set of containers for tests to run against, which makes it running tests against multiple environments a lot easier.

This is useful if you maintain open source projects.  For example, a blog engine could be tested against Node 0.10.x and 0.12.x, or you could even switch framework versions for Express/Rails/Django/etc.

The author includes examples for PHP, Node, and Python, and it seems like you could hook it up to a CI server easily enough.

###easy-livereload

Are you still searching for the perfect Express middleware for live reloading your app?  Daishi Kato sent in easy-livereload (GitHub: [dai-shi/easy-livereload](https://github.com/dai-shi/easy-livereload), License: _BSD_, npm: [easy-livereload](https://www.npmjs.com/package/easy-livereload)), a new module that uses LiveReload protocol 7.

If you haven't seen it before, then you might want to check out [the LiveReload homepage](http://livereload.com).  It's basically a protocol for updating client-side assets.  With Daishi's module, you'll get almost instant updates to client-side assets, but also server restarts as well.

Server restarts are managed with [node-dev](https://www.npmjs.com/package/node-dev).  One interesting thing about node-dev is it's compatible with [node-notifier](https://www.npmjs.com/package/node-notifier), so you can get desktop notifications when the server restarts.
