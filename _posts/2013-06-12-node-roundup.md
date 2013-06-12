---
layout: post
title: "Node Roundup: evilscan, pm2, connectr"
author: "Alex Young"
categories: 
- node
- modules
- security
- network
- cluster
- express
- connect
---

<div class="intro">
You can send in your Node projects for review through our <a href="/contact.html">contact form</a>.
</div>

###evilscan

It's finally here, TCP port scanning in Node!  evilscan (GitHub: [eviltik / evilscan](https://github.com/eviltik/evilscan), License: _GPLv3_, npm: [evilscan](https://npmjs.org/package/evilscan)) by Michel Soisson is a command-line tool, and has several interesting features, like control over the amount of concurrency, geolocation information, banner grabbing, and JSON output.

The author is focusing on _connect_ scans, but is interested in adding SYN scans and UDP support.  He's looking for contributors, and the project includes tests written with Mocha and Chai, so you really have no excuse not to help out!  I think it's great to see well-tested security-related modules.

###pm2

![pm2](/images/posts/pm2.png)

pm2 (GitHub: [Unitech / pm2](https://github.com/Unitech/pm2), License: _MIT_, npm: [pm2](https://npmjs.org/package/pm2)) by Alexandre Strzelewicz is a command-line process manager for Node.  It can be used to start a program as a cluster of processes, and then monitor the cluster's health, monitor the server itself (CPU/RAM/etc.), keep processes alive, log exceptions, and throttle programs that stop too quickly.

It also has tests written with Mocha, documentation, and [examples](https://github.com/Unitech/pm2/tree/master/examples).

###connectr

connectr (GitHub: [olalonde / connectr](https://github.com/olalonde/connectr), License: _MIT_, npm: [connectr](https://npmjs.org/package/connectr)) by Olivier Lalonde is a wrapper for Connect that allows middleware to be inserted at arbitrary points in the stack.  That means you can add middleware _before_ existing middleware.

It has a simple API: the `before` and `after` methods insert new middleware relative to other middleware, and it's also possible to add middleware to the top of the stack with `first`, or even based on an `index`.
