---
layout: post
title: "Node Roundup: 0.10.17, Defining Global Scripts in npm, loadtest"
author: "Alex Young"
categories: 
- node
- modules
- http
- benchmarking
- npm
---

###Node 0.10.17

[Node 0.10.17](http://blog.nodejs.org/2013/08/21/node-v0-10-17-stable/) is out, so it seems like we're back to weekly releases again.  This version updates uv, tls, stream, dgram, and readline.  The stream module fix makes errors raise exceptions when `'error'` listeners are removed, which seems like a _slight_ oversight to me...

###Defining Global Scripts in npm

Joe Sullivan sent in his post about how [global scripts are defined in popular npm modules](http://joesul.li/van/2013/08/npm-bin.html).  This is the kind of thing I like to see -- learning from the pros.  Joe summarises the common approaches at the end of the post.

###loadtest

loadtest (GitHub: [alexfernandez / loadtest](https://github.com/alexfernandez/loadtest), License: _MIT_, npm: [loadtest](https://npmjs.org/package/loadtest)) by Alex Fernández is a load testing module inspired by and partly compatible with [Apache ab](http://httpd.apache.org/docs/2.2/programs/ab.html).  It can be invoked as a command-line script or used as a module.

{% highlight javascript %}
var loadtest = require('loadtest');
var options = {
    url: 'http://localhost:8000',
    maxRequests: 1000,
};

loadtest.loadTest(options, function(error, result) {
  if (error) {
    return console.error('Error:', error);
  }

  console.log('Tests run successfully');
});
{% endhighlight %}

The callback is run when the requests have been made, or the specified number of seconds have elapsed.
