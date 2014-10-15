---
layout: post
title: "Node Roundup: node-android, typed-morph, stdio"
author: "Alex Young"
image: "/images/posts/nodeandroid.png"
categories:
- modules
- libraries
- node
- io
- streams
- iterator-protocol
- android
---

###node-android

[node-android](http://instantwebp2p.github.io/node-android/) (GitHub: [InstantWebP2P / node-android](https://github.com/InstantWebP2P/node-android), License: _MIT_) is a Node port for Android.  It uses libuvpp and libuv-java, and is mostly compatible with Node 0.10.x.  The authors haven't yet implemented the crypto modules, but it supports most of the other core modules as far as I can tell.

To use it you need to open the source in the Android Developer Tools plugin for Eclipse.

The people behind this project are based in Shanghai, and have also created some interesting peer-to-peer modules for Node.  I don't know what kind of commercial work they do, but there's a lot of activity on the [InstantWebP2P GitHub organisation](https://github.com/InstantWebP2P).

###typed-morph

typed-morph (GitHub: [pjsteam / typed-morph](https://github.com/pjsteam/typed-morph), License: _MIT_, npm: [typed-morph](https://www.npmjs.org/package/typed-morph)) by Damian Schenkelman is a set of iterators implemented using the [iterator protocol](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/The_Iterator_protocol) so you can map, reduce, and filter typed arrays without using intermediate arrays.

The evaluation is delayed until the results are consumed, so chained calls are basically lazy:

{% highlight javascript %}
var elements = new Uint16Array([1,4,7,10]);
var iter = wrap(elements)
  .map(function(e) { return e + 1; })
  .filter(function(e) { return e % 2 === 0; });

// at this point no processing has taken place
iter.reduce(function(value, current) { return value + current; }, 0);

expect(sum).to.equal(10);
{% endhighlight %}

###stdio

stdio (GitHub: [sgmonda / stdio](https://github.com/sgmonda/stdio), License: _MIT_, npm: [stdio](https://www.npmjs.org/package/stdio)) by Sergio García is a module for general standard input/output management.  You can use it for things like supporting command-line options, reading input by line, and prompting for input.

Command-line options are specified using a nice JavaScript object format:

{% highlight javascript %}
var stdio = require('stdio');
var ops = stdio.getopt({
  check: {key: 'c', args: 2, description: 'What this option means'},
  map: {key: 'm', description: 'Another description', mandatory: true},
  kaka: {key: 'k', args: 2, mandatory: true},
  ooo: {key: 'o'}
});
{% endhighlight %}

And options can also have a `multiple` flag, so you can support expressions like `-f a.txt -f b.txt -f c.txt`.

stdio can also automatically generate help, and it comes with Jasmine tests and documentation in the readme.
