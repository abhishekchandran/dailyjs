---
layout: post
title: "Five Minute Guide to Streams2"
author: "Alex Young"
categories: 
- streams
- streams2
- node
- 5min
---

Node 0.10 is the latest stable branch of Node.  It's the branch you should be using for Real Work&trade;.  The most significant API changes can be found in the [stream](http://nodejs.org/docs/latest/api/stream.html) module.  This is a quick guide to _streams2_ to get you up to speed.

###The Base Classes

There are now five base classes for creating your own streams: `Readable`, `Writable`, `Duplex`, `Transform`, and `PassThrough`.  These base classes inherit from `EventEmitter` so you can attach listeners and emit events as you normally would.  It's perfectly acceptable to emit custom events -- this might make sense, for example, if you're writing a streaming parser.  The parser could emit events like `'headers'` to indicate the headers have been parsed, perhaps for a CSV file.

To make your own `Readable` stream class, inherit from `stream.Readable` and implement the `_read(size)` method.  The `size` argument is "advisory" -- a lot of `Readable` implementations can safely ignore it.  Once your `_read` method has collected data from an underlying I/O source, it can send it by calling `this.push(chunk)` -- internally data will be placed into a queue so "clients" of your class can deal with it when they're ready.

The `Writable` class should also be inherited from, but this time a `_write(chunk, encoding, callback)` method should be implemented.  Once you've written data to the underlying I/O source, `callback` can be called, passing an error if required.

The `Duplex` class is like a `Readable` and `Writable` stream in one -- it allows data sources that transmit and receive data to be modelled.  This makes sense when you think about it -- TCP network sockets transmit and receive data.  To implement a `Duplex` stream, inherit from `stream.Duplex` and implement both the `_read` and `_write` methods.

The `Transform` class is useful for implementing parsers, like the CSV example I mentioned earlier.  In general, streams that change data in some way should be implemented using `stream.Transform`.  Although `Transform` sounds a bit like a `Duplex` stream, this time you'll need to implement a `_transform(chunk, encoding, callback)` method.  I've noticed several projects in the wild that use `Duplex` streams with a stubbed `_read` method, and I wondered if these would be better served by using a `Transform` class instead.

Finally, the `PassThrough` stream inherits from `Transform` to do... nothing.  It relays the input to the output.  That makes it ideal for sitting inside a `pipe` chain to spy on streams, and people have been using this to write tests or instrument streams in some way.

###Pipes

Pipes _must_ follow this pattern: `readable.pipe(writable)`.  As `Duplex` and `Transform` streams can both read _and_ write, they can be placed in either position in the chain.  For example, I've been using `process.stdin.pipe(csvParser).pipe(process.stdout)` where `csvParser` is a `Transform` stream.

###Inheritance

The general pattern for inheriting from the base classes is as follows:

1. Create a constructor function that calls the base class using `baseClass.call(this, options)`
2. Correctly inherit from the base class using `Object.create` or `util.inherits`
3. Implement the required underscored method, whether it's `_read`, `_write`, or `_transform`

Here's a quick `stream.Writable` example:

{% highlight javascript %}
var stream = require('stream');

GreenStream.prototype = Object.create(stream.Writable.prototype, {
  constructor: { value: GreenStream }
});

function GreenStream(options) {
  stream.Writable.call(this, options);
}

GreenStream.prototype._write = function(chunk, encoding, callback) {
  process.stdout.write('\u001b[32m' + chunk + '\u001b[39m');
  callback();
};

process.stdin.pipe(new GreenStream());
{% endhighlight %}

###Forwards Compatibility

If you want to use _streams2_ with Node 0.8 projects, then [readable-stream](https://github.com/isaacs/readable-stream) provides access to the newer APIs in an npm-installable module.  Since the `stream` core module is implemented in JavaScript, then it makes sense that the newer API can be used in Node 0.8.

Some open source module authors are including `readable-stream` as a dependency and then conditionally loading it:

{% highlight javascript %}
var PassThrough = require('stream').PassThrough;

if (!PassThrough) {
  PassThrough = require('readable-stream/passthrough');
}
{% endhighlight %}

This example is taken from [until-stream](https://github.com/EvanOxfeld/until-stream/blob/master/until.js).

###Streams2 in the Wild

There are some interesting open source projects that use the new streaming API that I've been collecting on GitHub.  [multiparser](https://github.com/jessetane/multiparser) by Jesse Tane is a `stream.Writable` HTML form parser.  [until-stream](https://github.com/EvanOxfeld/until-stream) by Evan Oxfeld will pause a stream when a certain signature is reached.

[Hiccup](https://github.com/naomik/hiccup) by naomik uses the new streams API to simulate sporadic throughput, and the same author has also released [bun](https://github.com/naomik/bun) which can help combine pipes into composable units, and [Burro](https://github.com/naomik/burro) which can package objects into length-prefixed JSON byte streams.  Conrad Pankoff used Burro to write [Pillion](https://github.com/deoxxa/pillion), which is an RPC system for object streams.

There are also less esoteric modules, like [csv-streamify](https://github.com/klaemo/csv-stream) which is a CSV parser.
