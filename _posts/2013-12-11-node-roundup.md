---
layout: post
title: "Node Roundup: parse5, redis-timeseries, request-as-curl"
author: Alex Young
categories:
- node
- modules
- curl
- html
- parsing
- redis
- statistics
---

###parse5

parse5 (GitHub: [inikulin / parse5](https://github.com/inikulin/parse5), License: _MIT_, npm: [parse5](https://npmjs.org/package/parse5)) by Ivan Nikulin is a new HTML5 parser, based on the WhatWG HTML5 standard.  It was built for a commercial project called [TestCafé](http://testcafe.devexpress.com/), when the authors found other HTML5 parsers to be too slow or inaccurate.

It's used like this:

{% highlight javascript %}
var Parser = require('parse5').Parser;
var parser = new Parser();
var document = parser.parse('<!DOCTYPE html><html><head></head><body>Hi there!</body></html>')
var fragment = parser.parseFragment('<title>Parse5 is &#102;&#117;&#99;&#107;ing awesome!</title><h1>42</h1>');
{% endhighlight %}

I had a look at the source, and it doesn't look like it was made with a parser generator.  It has a preprocessor, tokenizer, and special UTF-8 handling.  There are no dependencies, other than [nodeunit](nodeunit) for testing.  The tests were derived from [html5lib](https://github.com/html5lib), and include over 8000 test cases.

If you wanted to use it, you'll probably need to write a "tree adapter".  Ivan has included an [example tree adapter](https://github.com/inikulin/parse5/blob/master/lib/default_tree_adapter.js), which reminds me of writing SAX parser callbacks.

Ivan also sent in [mods](https://github.com/inikulin/mods), which is a module system designed to need less boilerplate than AMD-style libraries.

###Redis Time Series

Tony Sokhon sent in redis-timeseries (GitHub: [tonyskn / node-redis-timeseries](https://github.com/tonyskn/node-redis-timeseries), License: _MIT_, npm: [redis-timeseries](https://npmjs.org/package/redis-timeseries)), a project for managing time series data.  I've used Redis a few times as a data sink for projects that need realtime statistics, and I always found it worked well for the modest amounts of data my projects generated.  This project gives things a bit more structure -- you can create instances of time series and then record hits, then query them later.

A time series has a granularity, so you can store statistics at whatever resolution you require: `ts.getHits('your_stats_key', '1second', ts.minutes(3), callback)`.  This module is used by Tony's [dashboard](https://github.com/tonyskn/node-dashboard) project, which can be used to make a realtime dashboard.

###request-as-curl

request-as-curl (GitHub: [azproduction / node-request-as-curl](https://github.com/azproduction/node-request-as-curl), License: _BSD_, npm: [request-as-curl](https://npmjs.org/package/request-as-curl)) by Mikhail Davydov serialises options for `http.ClientRequest` into an equivalent `curl` command.  It also works for Express.

{% highlight javascript %}
// http.ClientRequest:
var req = request('http://google.com/', {method: 'POST', json: data}, function (error, response, expected) {
  curlify(req.req, data);
  // curl 'http://google.com' -H 'accept: application/json' -H 'content-type: application/json' -H 'connection: keep-alive' --data '{"data":"data"}' --compressed
});

// Express:

app.get('/', function (req) {
  curlify(req);
  // curl 'http://localhost/pewpew' -H 'x-real-ip: 127.0.0.1' -H etc...
});
{% endhighlight %}

I imagine Mikhail has been using this so he can replicate requests based on logs to aid in debugging.
