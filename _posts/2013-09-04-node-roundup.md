---
layout: post
title: "Node Roundup: Forky, dsjslib, Node-huxley"
author: "Alex Young"
categories: 
- node
- modules
- testing
- cluster
- data-structures
---

###Forky

Forky (GitHub: [brianc / node-forky](https://github.com/brianc/node-forky), License: _MIT_, npm: [forky](https://npmjs.org/package/forky)) by Brian M. Carlson is a wrapper around the `cluster` module to make it easier to use and test.

The `forky` function loads workers based on the number of cores on your system.  If any of the workers dies, Forky will spawn another one:

> The best way to handle unexpected errors in node is to shut down your process and spawn a new one. Forky makes clean process shutdown and respawn easy as pie.

###dsjslib

[dsjslib](http://monmohan.github.io/dsjslib/) (GitHub: [monmohan / dsjslib](https://github.com/monmohan/dsjslib), License: _MIT_, npm: [dsjslib](https://npmjs.org/package/dsjslib)) by Monmohan Singh is a collection of common data structures and utility functions.

It includes:

* Cache: An in-memory cache implementation, inspired by Google's [Guava project](https://code.google.com/p/guava-libraries/)
* AVL Tree: Map-like functionality backed by a balanced tree
* BTree
* RWayTrie: A data structure for fast retrieval of values associated with string keys
* TernarySearchTrie: Similar to RWayTrie, based on Algorithms, 4th Edition by Robert Sedgewick and Kevin Wayne

It includes unit tests, so you can get a feel for each API and see how the classes are meant to be used.

###Node-huxley

Node-huxley (GitHub: [chenglou / node-huxley](https://github.com/chenglou/node-huxley), License: _MIT_, npm: [huxley](https://npmjs.org/package/huxley)) by Cheng Lou is a port of Instagram's [Huxley](https://github.com/facebook/huxley) project.  It allows sequences of events in a web application to be recorded and compared against screenshots.

Huxley was originally designed for tracking "visual regressions in web applications":

> Huxley is a test-like system for catching visual regressions in Web applications. It was built by Pete Hunt with input from Maykel Loomans at Instagram.

