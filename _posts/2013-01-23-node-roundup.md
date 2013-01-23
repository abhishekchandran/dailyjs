---
layout: post
title: "Node Roundup: 0.8.18, Thrill, analytics-node, Hulkster"
author: "Alex Young"
categories: 
- node
- modules
---

<div class="intro">
You can send in your Node projects for review through our <a href="/contact.html">contact form</a> or <a href="http://twitter.com/dailyjs">@dailyjs</a>.
</div>

###Node 0.8.18

[Node 0.8.18](http://blog.nodejs.org/2013/01/18/node-v0-8-18-stable/) is out, and [0.9.7](http://blog.nodejs.org/2013/01/18/node-v0-9-7-unstable/) was released on the same day as well.

I'm still tracking those stream module changes in the 0.9 branch, and this release has a fix for [handling large reads from push-streams](https://github.com/joyent/node/commit/14e8f806deca0475da31676fd9952d341b8f50e5).  Although the commit isn't dramatic, the test case seems to thoroughly cover the problems outlined in the commit message.

###Thrill

![Thrill](/images/posts/thrill.png)

Ozan Turgut sent in [Thrill](http://thrilljs.com/) (GitHub: [ozanturgut / thrill](https://github.com/ozanturgut/thrill), License: _Apache 2.0_, npm: [thrill](https://npmjs.org/package/thrill)), a new test runner that can drive browsers over the network.  A server runs tests using pools of browsers powered by Selenium Grid, Sauce Labs, or Browser Stack.

There's a [quick start guide](https://github.com/ozanturgut/thrill/wiki/Use) that explains how to install the requirements and run some tests using Jasmine, but you could use another test framework if you prefer.

The tests will be run in a browser after "connecting" it to a server.  Once this is done, tests can be run using the command-line tool, `thrill`.  That means you can run a standard Jasmine spec file with `thrill runner.html` and it'll run on all of the connected browsers.

The documentation for the project makes all of this easy to follow, so if you want to try it out take a look at taht [quick start guide](https://github.com/ozanturgut/thrill/wiki/Use).

###analytics-node

[analytics-node](https://segment.io/libraries/node) (GitHub: [segmentio / analytics-node](https://github.com/segmentio/analytics-node), License: _MIT_, npm: [analytics-node](https://npmjs.org/package/analytics-node)) is a Node client for [Segment.io](https://segment.io/).  It can be used to send data to various analytics services with the same API as the extremely popular [analytics.js](https://github.com/segmentio/analytics.js) library.

###Hulkster

Hulkster (GitHub: [neoziro / hulkster](https://github.com/neoziro/hulkster), License: _MIT_, npm: [hulkster](https://npmjs.org/package/hulkster)) by Greg Bergé is a [Hogan.js](http://twitter.github.com/hogan.js/) wrapper that adds extra functionality.  It can be used as a Node module, or as a command-line tool.

Hulkster adds lots of command-line options, like control over the format (json or js), the export variable used, AMD-style, and minification.  The author has included some Mocha tests to make sure these new features work as intended.

