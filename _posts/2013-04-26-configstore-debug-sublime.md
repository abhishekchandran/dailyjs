---
layout: post
title: "Yeoman Configstore, Debug.js, Sublime JavaScript Refactoring"
author: "Alex Young"
categories: 
- yeoman
- libraries
- browser
- node
- debugging
- editors
---

###Configstore

Sindre Sorhus sent in configstore (GitHub: [yeoman / configstore](https://github.com/yeoman/configstore), License: _BSD_, npm: [configstore](https://npmjs.org/package/configstore)), a small module for storing configuration variables without worrying about where and how.  The underlying data file is YAML, and stored in `$XDG_CONFIG_HOME`.

`Configstore` instances are used with a simple API for getting, setting, and deleting values:

{% highlight javascript %}
var Configstore = require('configstore');
var packageName = require('./package').name;

var conf = new Configstore(packageName, { foo: 'bar' });

conf.set('awesome', true);
console.log(conf.get('awesome'));  // true
console.log(conf.get('foo'));      // bar

conf.del('awesome');
console.log(conf.get('awesome'));  // undefined
{% endhighlight %}

The [Yeoman repository on GitHub](https://github.com/yeoman) has many more interesting server-side and client-side modules -- currently most projects are related to client-side workflow, but given the discussions on [Yeoman's Google+](https://plus.google.com/101063139999404044459/posts) account I expect there will be an increasing number of server-side modules too.

###Debug.js

Jerome Etienne has appeared on DailyJS a few times with his WebGL libraries and tutorials.  He recently released [debug.js](http://blog.jetienne.com/blog/2013/04/23/debug-dot-js-global-detection/) (GitHub: [jeromeetienne / debug.js](https://github.com/jeromeetienne/debug.js), License: _MIT_), which is a set of tools for browser and Node JavaScript debugging.

The tutorial focuses on global leak detection, which is able to display a trace that shows where the leak originated.  Another major feature is strong type checking for properties and function arguments.

Methods can also be marked as deprecated, allowing debug.js to generate notifications when such methods are accessed.

More details can be found on the [debug.js](http://jeromeetienne.github.io/debug.js/) project page.

###Sublime Text Refactoring Plugin

Stephan Ahlf sent in his [Sublime Text Refactoring Plugin](http://saquery.com/sublime-text-refactoring-plugin/) (GitHub: [s-a / sublime-text-refactor](https://github.com/s-a/sublime-text-refactor), License: _MIT/GPL_).  The main features are method extraction, variable and function definition navigation, and renaming based on scope.

The plugin uses Node, and has some unit tests written in Mocha.  The author is planning to add more features (the readme has a to-do list).
