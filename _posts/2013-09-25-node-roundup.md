---
layout: post
title: "Node Roundup: 0.10.19, klei-migrate, division"
author: "Alex Young"
categories: 
- node
- modules
- npm
- cluster
- databases
---

###Node 0.10.19 Released

[Node 0.10.19](http://blog.nodejs.org/2013/09/24/node-v0-10-19-stable/) was released yesterday.  This version updates uv, npm, and also some core modules: readline, stream, and tls.

When you read `uv: Upgrade to v0.10.17` in the release notes, don't you wonder what that means?  If you're interested in the changes in libuv, all you need to do is checkout the relevant tag from GitHub.  In this case it's [libuv/tree/v0.10.17](https://github.com/joyent/libuv/tree/v0.10.17):

{% highlight text %}
2013.09.25, Version 0.10.17 (Stable)
Changes since version 0.10.16:

* build: remove GCC_WARN_ABOUT_MISSING_NEWLINE (Ben Noordhuis)
* darwin: fix 10.6 build error in fsevents.c (Ben Noordhuis)
{% endhighlight %}

If you switch to [0.11.13](https://github.com/joyent/libuv/blob/v0.11.13/ChangeLog), the latest unstable release, you'll see a whole load of interesting changes -- `uv_fs_stat` has been rewritten, `FSEventStream` is now shared between multiple filesystem watchers, so it removes the limit on the maximum number of file watchers that can be created on OS X.  These are just some random changes that caught my eye, there are plenty more.

These libuv changes have a direct impact on Node's filesystem and networking modules, so it's worth paying attention if you can.

###klei-migrate

klei-migrate (GitHub: [klei-dev / migrate](https://github.com/klei-dev/migrate), License: _MIT_, npm: [klei-migrate](https://npmjs.org/package/klei-migrate)) by Joakim Bengtson is a database independent migration command-line tool.  It also works as a module, and has a [Grunt plugin](https://github.com/klei-dev/grunt-klei-migrate).

Migrations can be created with `klei-migrate new`, and then run with `klei-migrate run`.  There are also other commands designed to help deal with switching between git branches, which can be tied into a post-checkout hook.

###division

division (GitHub: [codename- / division](https://github.com/codename-/division), License: _MIT_, npm: [division](https://npmjs.org/package/division)) is another cluster module wrapper:

> division provides an easy to use, chainable API, with some built-in extensions (like signals handlers) and is built with performance, zero-downtime restart (of workers), stability and simplicity in mind. The main advantage of division is that it does not depend of other modules - less dependencies equal less places where something could went wrong.

{% highlight javascript %}
var division = require('division');
var cluster = new division();

// Configuration for development environment
cluster.configure('development', function() {
  // Put your development configuration here
  cluster.set('args', ['--some-process-args', 'send-to-workers']);
});

cluster.configure('production', function() {
  // Put your production configuration here
  cluster.enable('silent');
});

cluster.configure(function() {
  this.set('path', 'app.js');
});

cluster.set('size', 2);
cluster.use('debug').use('signals');

// Start your application as a cluster!
cluster.run(function() {
  // `this` is pointing to the Master instance
});
{% endhighlight %}

