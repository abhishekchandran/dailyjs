---
layout: post
title: "Node Roundup: redis-stream, DataGen, Cushion"
author: "Alex Young"
categories:
- node
- modules
- libraries
- streams
- redis
- couchdb
---

<div class="intro">
You can send in your Node projects for review through our <a href="/contact.html">contact form</a> or <a href="http://twitter.com/dailyjs">@dailyjs</a>.
</div>

###redis-stream

[redis-stream](https://github.com/tblobaum/redis-stream) (License: _MIT_, npm: [redis-stream](https://npmjs.org/package/redis-stream)) by Thomas Blobaum is a stream-based wrapper around the [Redis protocol](http://redis.io/topics/protocol).  It's actually an extremely lightweight module, but the author has included tests and some interesting examples.  The standard Node stream methods work, so data can be piped:

{% highlight javascript %}
var Redis = require('redis-stream')
  , client = new Redis(6379, localhost, 0)
  , rpop = client.stream('rpop');

rpop.pipe(process.stdout);
rpop.write('my-list-key');
{% endhighlight %}

This doesn't just apply to `rpop`, other [Redis commands](http://redis.io/commands) will also work in a similar way.

###DataGen

[DataGen](http://blog.cliffano.com/2012/07/08/datagen-generate-large-test-data-files-like-a-boss/) (GitHub: [cliffano / datagen](https://github.com/cliffano/datagen), License: _MIT_, npm: [datagen](https://npmjs.org/package/datagen)) by Cliffano Subagio is a multi-process test data file generator.  It can be used to generate files in various formats, including CSV and JSON, based on template files that describe the output.  Random numbers, dates, and strings can be generated.

The underlying random data generation is based on the [Faker](https://npmjs.org/package/Faker) library, and Mocha tests are included.


###Cushion

[Cushion](http://zoddy.github.com/cushion/) (GitHub: [Zoddy / cushion](https://github.com/Zoddy/cushion), License: _MIT_, npm: [cushion](https://npmjs.org/package/cushion)) by André Kussmann is a CouchDB API.  It has Node-friendly asynchronous wrappers around the usual CouchDB API methods, and it also supports low-level requests by calling `cushion.request`.
Fetching documents returns a document object that can be modified and saved like this:

{% highlight javascript %}
var doc = db.document('id');
doc.load(function(err, document) {
  document.body({ name: 'Quincy' });
  document.save();
});
{% endhighlight %}

Designs and users can also be fetched and manipulated.
