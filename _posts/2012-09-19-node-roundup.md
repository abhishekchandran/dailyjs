---
layout: post
title: "Node Roundup: mongo-lite, smog, sshfs-node"
author: "Alex Young"
categories:
- node
- modules
- libraries
- filesystem
- mongo
---

<div class="intro">
You can send in your Node projects for review through our <a href="/contact.html">contact form</a> or <a href="http://twitter.com/dailyjs">@dailyjs</a>.
</div>

###mongo-lite

[mongo-lite](http://alexeypetrushin.github.com/mongo-lite/docs/index.html) (GitHub: [alexeypetrushin / mongo-lite](https://github.com/alexeypetrushin/mongo-lite), License: _MIT_, npm: [mongo-lite](https://npmjs.org/package/mongo-lite)) by Alexey Petrushin aims to simplify MongoDB by removing the need for most callbacks, adding reasonable defaults like safe updates, and offering optional compact IDs.

The chainable API looks more like MongoDB's command-line interface:

{% highlight javascript %}
var db = require('mongo-lite').connect('mongodb://localhost/test', ['posts', 'comments']);
db.posts.insert({ title: 'first' }, function(err, post) {
  // Use post
});
{% endhighlight %}

There's also a Fiber-based API, so it can be used in a synchronous fashion.

###smog

[smog](https://github.com/wearefractal/smog) (License: _MIT_, npm: [smog](https://npmjs.org/package/smog)) from Fractal is a web-based MongoDB interface.  It displays collections, and allows them to be sorted and edited.  It also supports administration features, like shutting down servers, CPU/bandwidth usage graphs, and replica set management.

It's built with Connect, and there's an experimental GTK+ desktop interface made with the [pane](https://npmjs.org/package/pane) module by the same authors.

###sshfs-node

[sshfs-node](https://github.com/cbou/sshfs-node) (License: _MIT_, npm: [sshfs-node](https://npmjs.org/package/sshfs-node)) by Charles Bourasseau allows remote filesystems to be mounted using SSH.  It uses [sshfs](http://fuse.sourceforge.net/sshfs.html) and requires keys for authentication, rather than passwords.

It comes with Vows tests, and the same author has also released [fs2http](https://github.com/cbou/fs2http).
