---
layout: post
title: "Node Roundup: 0.8.21, Node Redis Pubsub, node-version-assets"
author: "Alex Young"
categories: 
- node
- modules
- redis
- databases
- grunt
---

<div class="intro">
You can send in your Node projects for review through our <a href="/contact.html">contact form</a>.
</div>

###Node 0.8.21

[Node 0.8.21](http://blog.nodejs.org/2013/02/25/node-v0-8-21-stable/) is out.  There are fixes for the http and zlib modules, so it's safe and sensible to update.

###Node Redis Pubsub

Louis Chatriot sent in NRP (Node Redis Pubsub) (GitHub: [louischatriot / node-redis-pubsub](https://github.com/louischatriot/node-redis-pubsub), License: _MIT_, npm: [node-redis-pubsub](https://npmjs.org/package/node-redis-pubsub)) which provides a Node-friendly API to Redis' [pub/sub](http://redis.io/topics/pubsub) functionality.  The API looks a lot like `EventEmitter`, so if you need to communicate between separate processes and you're using Redis then this might be a good solution.

Louis says he's using it at [tl;dr](http://tldr.io/) in production, and the project comes with tests.

###node-version-assets

node-version-assets (GitHub: [techjacker / node-version-assets](https://github.com/techjacker/node-version-assets), License: _MIT_, npm: [node-version-assets](https://npmjs.org/package/node-version-assets)) by Andrew Griffiths is a module for hashing assets and placing the hash in the filename.  For example, `styles.css` would become `styles.7d47723e723251c776ce9deb5e23062b.css`.  This is implemented using Node's file system streams, and the author has provided a Grunt example in case you want to invoke it that way.

