---
layout: post
title: "Node Roundup: HTTP DoS Fixed, Flocon, Trans"
author: "Alex Young"
categories: 
- node
- modules
- uuid
- json
---

###Node DoS Fixes

This week two maintenance releases of Node were rolled out to fix a DoS vulnerability in the HTTP module.

* [DoS Vulnerability](http://blog.nodejs.org/2013/10/22/cve-2013-4450-http-server-pipeline-flood-dos/)
* [Node 0.10.21](http://blog.nodejs.org/2013/10/18/node-v0-10-21-stable/)
* [Node 0.8.26](http://blog.nodejs.org/2013/10/18/node-v0-8-26-maintenance/)

###Flocon

I seem to find myself generating a lot of unique IDs lately.  Flocon (GitHub: [Yosee / flocon](https://github.com/Yosee/flocon), License: _MIT_, npm: [flocon](https://npmjs.org/package/flocon)) from [Yosee](https://www.yosee.com/) is a 64-bit unique ID generator, written in C++.  It's currently considered experimental by the authors but comes with unit tests.

Flocon returns IDs synchronously as strings with `flocon.snow()`, and the algorithm used is based on [Twitter's Snowflake service](https://github.com/twitter/snowflake/).

There are also some [benchmarks of the flocon module](https://github.com/Yosee/flocon/tree/master/bench) so you can compare it to other projects.

###Trans

Gabriel Adomnicai sent in "trans" (GitHub: [gabesoft / trans](https://github.com/gabesoft/trans), License: _MIT_, npm: [trans](https://npmjs.org/package/trans)), a module for transforming objects.  Given some JSON, trans can group and modify objects by using a chainable API:

{% highlight javascript %}
var trans = require('trans');
var data = [
  { a: { b: 'fbc' }, c: 1 }
, { a: { b: 'foo' }, c: 3 }
, { a: { b: 'fde' }, c: 2 }
, { a: { b: 'def' }, c: 3 }
, { a: { b: 'ghk' }, c: 4 }
];

trans(data)
  .group('a.b', 'c', ['charAt', 0], 'toUpperCase')
  .sortf('value')
  .sort('key')
  .value();

/*
[ { key: 'D', value: [ 3 ] },
  { key: 'F', value: [ 1, 2, 3 ] },
  { key: 'G', value: [ 4 ] } ]
*/
{% endhighlight %}

Each of the methods is documented in the readme, and Gabriel has included tests as well.
