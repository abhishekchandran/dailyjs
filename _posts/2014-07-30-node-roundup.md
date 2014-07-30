---
layout: post
title: "Node Roundup: Building Node.js Together, node-libnmap, httpolyglot"
author: "Alex Young"
categories:
- node
- modules
- libraries
- network
- security
- http
---

###Building Node.js Together

TJ Fontaine wrote about Node from a release management perspective on the official Node blog, in [Building Node.js Together](http://blog.nodejs.org/2014/07/29/building-nodejs-together/).  It covers documentation, code quality, and the growing team of core contributors and contributors that are employed full-time to work on Node:

> For instance, Chris Dickinson was recently hired to work full time on Node.js, and has expressed interest in working on the current and future state of streams. But it's not who employs Chris that makes him an ideal candidate, but it will be the quality of his contributions, and his understanding of the ethos of Node.js. That's how we find members of the team.

###node-libnmap

The [evilscan](https://www.npmjs.org/package/evilscan) module uses JavaScript to enumerate over TCP ports.  node-libnmap (GitHub: [jas- / node-libnmap](https://github.com/jas-/node-libnmap), License: _MIT_, npm: [node-libnmap](https://www.npmjs.org/package/node-libnmap)) by Jason Gerfen is an alternative that uses the nmap binary.

It will return results as JavaScript objects, so you should be able to process the output fairly easily.  A basic scan looks like this:

{% highlight javascript %}
var libnmap = require('libnmap');

var opts = {
  range: ['localhost', '10.0.2.0/24', '192.168.2.0/25']
}

libnmap.nmap('scan', opts, function(err, report){
  if (err) throw err
  report.forEach(function(item){
    console.log(item[0])
  });
});
{% endhighlight %}

###httpolyglot

httpolyglot (GitHub: [mscdex / httpolyglot](https://github.com/mscdex/httpolyglot), License: _MIT_, npm: [httpolyglot](https://www.npmjs.org/package/httpolyglot)) by Brian White allows you to start a server that accepts both HTTP and HTTPS connections on the same port.

It works by sniffing the first byte of the stream to see if TLS is required:

{% highlight javascript %}
var firstByte = data[0];
socket.unshift(data);
if (firstByte < 32 || firstByte >= 127) {
  // tls/ssl
  this._tlsHandler(socket);
} else
  this.__httpSocketHandler(socket);
{% endhighlight %}
