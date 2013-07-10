---
layout: post
title: "Node Roundup: 0.10.13, Node Linux, Tree Model"
author: "Alex Young"
categories: 
- node
- modules
- trees
- data-structures
- linux
---

<div class="intro">
You can send in your Node projects for review through our <a href="/contact.html">contact form</a>.
</div>

###Node 0.10.13

[Node 0.10.13](http://blog.nodejs.org/2013/07/09/node-v0-10-13-stable/) was released yesterday.  Updates include libuv, npm, and fixes for the following core modules: tls, http, zlib, and buffer.

####Node Linux

Corey Butler sent in node-linux (GitHub: [coreybutler / node-linux](https://github.com/coreybutler/node-linux), License: _MIT_, npm: [node-linux](https://npmjs.org/package/node-linux)), which is a follow up to [node-windows](https://github.com/coreybutler/node-windows) and [node-mac](https://github.com/coreybutler/node-mac).  The Mac and Windows versions provided an integration layer for working with OS-specific features like event logging and service management.  The Linux version creates System V init.d files that run Node scripts and daemons.

The author is planning to add systemd and upstart script generation, and notes in the readme that he'd like contributions in those areas if possible.

###tree-model-js

![tree-model-js](/images/posts/tree-model-js.png)

[tree-model-js](http://jnuno.com/tree-model-js/) (GitHub: [joaonuno / tree-model-js](https://github.com/joaonuno/tree-model-js), License: _MIT_, npm: [tree-model](https://npmjs.org/package/tree-model)) by Joao Nuno Silva is a module for manipulating and traversing tree-like structures.  It's available for Node, but also supports browsers and AMD.

Trees can be defined with a JSON-friendly syntax:

{% highlight javascript %}
var tree = new TreeModel();
var root = tree.parse({
  id: 1,
  children: [{
      id: 11,
      children: [{id: 111}]
    }, {
      id: 12,
      children: [{id: 121}, {id: 122}]
    }, {
      id: 13
    }
  ]
});
{% endhighlight %}

Nodes can then be traversed with `.walk`, removed with `.drop`, and added with `.addChild`.
