---
layout: post
title: "Caress, cjs2web, zoe.js"
author: Alex Young
categories:
- libraries
- oo
- touch
- commonjs
---

###Caress

[Caress](http://caressjs.com/) (GitHub: [ekryski / caress-server](https://github.com/ekryski/caress-server), License: _MIT_, npm: [caress-server](https://npmjs.org/package/caress-server)) by Eric Kryski converts [TUIO](http://tuio.org/) events to browser events (W3C Touch Events version 2), allowing desktop browsers to be driven by multitouch devices.  This includes Apple's Magic Trackpad, Android, and iOS devices.

Caress uses Node and Socket.IO to send TUIO messages to the browser -- this is usually done using UDP, but Node and Socket.IO seem to work well.  Since Caress can be used with the Magic Trackpad, it might work well as a shortcut for testing touch-based interfaces during development.

###cjs2web

cjs2web (GitHub: [cjs2web](https://github.com/alexlawrence/cjs2web), License: _MIT_, npm: [cjs2web](https://npmjs.org/package/cjs2web)) by Alex Lawrence is a CommonJS module-to-browser translation tool.  It currently supports mapping local modules, and the `exports` object (including `module.exports`).  It doesn't support Node's `process` and `global` modules, so it's useful for lightweight porting of browser-friendly code.  This is in contrast to something like [OneJS](https://github.com/azer/onejs) that actually aims to create a Node-like environment in the browser.

Jasmine specs are included, and the Grunt build script used to run them.

###zoe.js

[zoe.js](http://zoejs.org/) (GitHub: [zestjs / zoe](https://github.com/zestjs/zoe), License: _MIT_, npm: [zoe](https://npmjs.org/package/zoe), component: `zestjs/zoe`) by Guy Bedford is a Node/AMD/browser library for working with multiple inheritance:

> The basic principle is that inheritance is a form of object extension. A core object is extended with a number of implemented definitions. When that object is extended, a new object is created implementing the core definitions as well as any new definitions. This is the inheritance system of `zoe.create`.

Objects created this way can be configured with "function chains", which allows the library to support asynchronous code and various forms of the observer pattern.

Basic object extension uses `zoe.create`:

{% highlight javascript %}
var baseClass = {
  hello: 'world'
};

var derivedClass = zoe.create([baseClass], {
  another: 'property'
});
{% endhighlight %}

If an `_extend` property is supplied, zoe will use it to apply various rules.  In this example, chaining is used which will cause both `greet` methods to run:

{% highlight javascript %}
var greetClass = {
  _extend: {
    greet: 'CHAIN'
  },
  greet: function() {
    return 'howdy';
  }
};

var myClass = zoe.create([greetClass], {
  greet: function() {
    alert('greeting');
  }
});

myClass.greet();
{% endhighlight %}

