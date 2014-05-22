---
layout: post
title: "Node Roundup: webpack, Mitm.js, musicmetadata"
author: "Alex Young"
categories:
- node
- modules
- npm
- build-systems
- network
---

###webpack

![webpack](/images/posts/webpack.png)

Vignesh Anand sent in [webpack](http://webpack.github.io/) (GitHub: [webpack](https://github.com/webpack/webpack), License: _MIT_, npm: [webpack](https://github.com/webpack/webpack)) by Tobias Koppers.  It's a bundler for CommonJS and AMD packages, based around asynchronous I/O, and supports preprocessors like CoffeeScript.

With webpack you can load chunks of dependencies on demand, so you can reduce the initial payload.  It only supports JavaScript by default, but there are modules for loading resources like CSS (`css-loader`).  To understand how it works, the [getting started tutorial](http://webpack.github.io/docs/tutorials/getting-started/) provides a high-level overview.

Vignesh pointed out that [Instagram uses webpack](https://github.com/webpack/webpack/issues/139), and it already has a lot of support on GitHub.

> Just wanted to leave a little thank you and share the exciting news that instagram.com is now building and serving all of its js and css assets with webpack :). @sokra you've been an awesome help in getting this all working, and our build step is so much cleaner and quicker because of it.

###Mitm.js

Mitm (GitHub: [moll / node-mitm](https://github.com/moll/node-mitm), License: _LAGPL_, npm: [mitm](https://www.npmjs.org/package/mitm)) by Andri Möll is a module for intercepting and mocking outgoing TCP and HTTP connections.  Running `Mitm()` will enable mocking for sockets, and it returns an object that allows mocking to be disabled:

{% highlight javascript %}
var Mitm = require('mitm');
var mitm = Mitm();

// Later:
mitm.disable()
{% endhighlight %}

The documentation has more examples, including how to handle HTTP requests during testing.

###musicmetadata

musicmetadata (GitHub: [leetreveil / musicmetadata](https://github.com/leetreveil/musicmetadata/), npm: [musicmetadata](https://www.npmjs.org/package/musicmetadata)) by Lee Treveil is a streaming metadata parser for music files:

{% highlight javascript %}
var fs = require('fs');
var mm = require('musicmetadata');

// create a new parser from a node ReadStream
var parser = mm(fs.createReadStream('sample.mp3'));

// listen for the metadata event
parser.on('metadata', function(result) {
  console.log(result);
});
{% endhighlight %}

The project is a fork of [node-id3](https://github.com/aadsm/node-id3) by António Afonso.
