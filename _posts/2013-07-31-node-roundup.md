---
layout: post
title: "Node Roundup: 0.10.15, IntervalStream, StreamToMongo, fileswap-stream"
author: "Alex Young"
categories: 
- node
- modules
- fs
- streams
---

<div class="intro">
You can send in your Node projects for review through our <a href="/contact.html">contact form</a>.
</div>

###0.10.15

[Node 0.10.15](http://blog.nodejs.org/2013/07/25/node-v0-10-15-stable/) was released last week, which quickly followed [0.10.14](http://blog.nodejs.org/2013/07/25/node-v0-10-14-stable/).  The newer release [adds a fix for `process.getuid`](https://github.com/joyent/node/commit/015ec05272cf9742bcfaea1f8884e81c31285f5f), to address an issue on Mac OS X:

> This commit should unbreak npm on OS X - it's hitting the new 'uid must be an unsigned int' check when installing as e.g. user 'nobody' (which has an UID of -2 in /etc/passwd or 4294967294 when cast to an uid_t.)

Version 0.10.14 fixed bugs in `os`, `url`, and upgraded npm and uv.

###IntervalStream

node-interval-stream (GitHub: [czzarr / node-interval-stream](https://github.com/czzarr/node-interval-stream), License: _MIT_, npm: [interval-stream](https://npmjs.org/package/interval-stream)) by Stanislas Marion is a simple module that provides a `Transform` stream that triggers events based on an interval.  The author's example combines `IntervalStream` with `request` to display the results of a large download every 2 seconds:

{% highlight javascript %}
var request = require('request');
var IntervalStream  = require('interval-stream');
var is = new IntervalStream(2000); // emit every 2 seconds

request('http://example.com/large_data_set.json')
  .pipe(is)
  .pipe(process.stdout);
{% endhighlight %}

###StreamToMongo

StreamToMongo (GitHub: [czzarr / node-stream-to-mongo](https://github.com/czzarr/node-stream-to-mongo), License: _MIT_, npm: [stream-to-mongo](https://npmjs.org/package/stream-to-mongo)), also by Stanislas Marion, allows data to be streamed to MongoDB.  This could be used to stream JSON data directly into a database.  The example in the readme uses the npm registry, effectively allowing you to create a structured local cache in Mongo of all the module metadata on npm.

###fileswap-stream

Finally, fileswap-stream (GitHub: [bpostlethwaite / fileswap-stream](https://github.com/bpostlethwaite/fileswap-stream), License: _MIT_, npm: [fileswap-stream](https://npmjs.org/package/fileswap-stream)) by Ben Postlethwaite allows underlying file resources to be swapped.  This might be useful if you're streaming data to log files, and want to split the files:

> Write to a writable file-stream that swaps out its underlying file resources according to swapper and naming functions. This can be used for a persistent log or data stream - just stream to it 24/7 and let it swap out to new files whenever you trigger it to.

