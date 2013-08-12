---
layout: post
title: "Ground, Generators and Async Patterns in Node, Time Grunt"
author: "Alex Young"
categories: 
- node
- modules
- grunt
- typekit
- frameworks
- async
- es6
---

###Ground

[Ground](http://gnd.io/) (GitHub: [OptimalBits / ground](https://github.com/OptimalBits/ground), License: _MIT_) from OptimalBits is a web framework for Node that is written with TypeScript:

> In ground, most of the application logic is moved from the server to the client, whereas the server acts mostly as an scalable, efficient distributed storage and synchronization controller.

> It includes also some rather useful features such as a hierarchical routing system, an undo/redo manager, property and declarative bindings, reference counting and automatic synchronization between clients and servers. It is design to always deliver high performance and low memory consumption.

Grunt is used for building the client-side code and deploying it.  It uses models in the style of the Mongoose ODM, and most parts of the framework including models have event APIs.  Views are implemented using view models.

The documentation at [gnd.io](http://gnd.io/) includes more examples and demos.

###Generators and Async Patterns in Node

Gorgi Kosev sent in his essay, [Analysis of generators and other async patterns in node](http://spion.github.io/posts/analysis-generators-and-other-async-patterns-node.html).  He looks at how generators work, how the code compares to other implementations (for example, promises), using a complexity measurement, and benchmarks of memory and execution time.

> The generator solution suspend is really fast. It incurred minimal overhead of about 50-80% running time. It's also roughly comparable with streamlinejs (when in raw callbacks mode).

###Time Grunt

time-grunt (GitHub: [sindresorhus / time-grunt](https://github.com/sindresorhus/time-grunt), License: _MIT_, npm: [time-grunt](https://npmjs.org/package/time-grunt)) by Sindre Sorhus displays the elapsed time of Grunt tasks:

{% highlight javascript %}
// Gruntfile.js
module.exports = function(grunt) {
  // require it at the top and pass in the grunt instance
  require('time-grunt')(grunt);

  grunt.initConfig();
  grunt.registerTask('default', []);
}
{% endhighlight %}
