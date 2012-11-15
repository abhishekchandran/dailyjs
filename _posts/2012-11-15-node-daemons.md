---
layout: post
title: "Node Daemon Architecture"
author: "Alex Young"
categories: 
- node
- unix
- daemons
---

I've been researching the architecture of [application layer](http://en.wikipedia.org/wiki/Application_layer) server implementations in Node.  I'm talking SMPT, IMAP, NNTP, Telnet, XMPP, and all that good stuff.

Node has always seemed like the perfect way to write network oriented daemons.  If you're a competent JavaScript developer, it unlocks powerful asynchronous I/O features.  In [The Architecture of Open Source Applications: nginx](http://www.aosabook.org/en/nginx.html) by Andrew Alexeev, the author explains nginx's design in detail -- in case you don't know, nginx is a HTTP daemon that's famous for solid performance.  Andrew's review states the following:

> It was actually inspired by the ongoing development of advanced event-based mechanisms in a variety of operating systems. What resulted is a modular, event-driven, asynchronous, single-threaded, non-blocking architecture which became the foundation of nginx code.

Furthermore,

> Connections are processed in a highly efficient run-loop in a limited number of single-threaded processes called workers. Within each worker nginx can handle many thousands of concurrent connections and requests per second.

Highly efficient run-loop and event-based mechanisms?  That sounds exactly like a Node program!  In fact, Node comes with several built-in features that make dealing with such an architecture a snap.

###Events

If you read DailyJS you probably know all about [EventEmitter](http://nodejs.org/docs/latest/api/all.html#all_class_events_eventemitter).  If not, then this is the heart of Node's event-based APIs.  Learn `EventEmitter` and [the Stream API](http://nodejs.org/docs/latest/api/all.html#all_stream) and you'll be able to easily learn Node's other APIs very quickly.

`EventEmitter` is the nexus of Node's APIs.  You'll see it underlying the network APIs, including the HTTP and HTTPS servers.  You can happily stuff it into your own classes with [util.inherits](http://nodejs.org/docs/latest/api/all.html#all_util_inherits_constructor_superconstructor) -- and you should!  At this point, many popular third-party Node modules use `EventEmitter` or one of its descendants as a base class.

If you're designing a server of some kind, it would be wise to consider basing it around `EventEmitter`.  And once you realise how common this is, you'll find all kinds of ways to improve the design of everything from daemons to web applications.  For example, if I need to notify disparate entities within an Express application that something has happened, knowing that Express mixes `EventEmitter` into the `app` object means I can do things like `app.on` and `app.emit` rather than requiring access to a global `app` object.

###Process

Guess what else is an instance of `EventEmitter`?  The [process](http://nodejs.org/docs/latest/api/all.html#all_process_1) global object.  It can be used to manage the current process -- including events for signals.

###Domain

[Domains](http://nodejs.org/docs/latest/api/all.html#all_domain) can be used to group I/O operations -- that means working with errors in nested callbacks is a little bit less painful:

> If any of the event emitters or callbacks registered to a domain emit an `error` event, or throw an error, then the domain object will be notified, rather than losing the context of the error in the `process.on('uncaughtException')` handler, or causing the program to exit with an error code.

Domains are currently experimental, but from my own experiences writing long-running daemons with Node, they definitely bring a level of sanity to my spaghetti code.

###Cluster

The [Cluster](http://nodejs.org/docs/latest/api/all.html#all_cluster) module is also experimental, but makes it easier to spawn multiple Node processes that share server ports.  These processes, or workers, can communicate using IPC ([Inter-process communication](http://en.wikipedia.org/wiki/Interprocess_communication)) -- all using the `EventEmitter`-based API you know and love.

###In the Wild

I've already mentioned that [Express](http://expressjs.com/) "mixes in" `EventEmitter`.  This is in contrast to the inheritance-based approach detailed in Node's documentation.  It's incorrect to say Express does this because it's actually done by [Connect, in connect.js](https://github.com/senchalabs/connect/blob/e0c0c5554a106b68fa0a28f4816d8c256e78e479/lib/connect.js):

{% highlight javascript %}
function createServer() {
  function app(req, res){ app.handle(req, res); }
  utils.merge(app, proto);
  utils.merge(app, EventEmitter.prototype);
  app.route = '/';
  app.stack = [];
  for (var i = 0; i < arguments.length; ++i) {
    app.use(arguments[i]);
  }
  return app;
};
{% endhighlight %}

The `utils.merge` method copies properties from one object to another:

{% highlight javascript %}
exports.merge = function(a, b){
  if (a && b) {
    for (var key in b) {
      a[key] = b[key];
    }
  }
  return a;
};
{% endhighlight %}

There's also a unit test that confirms that the authors intended to mix in `EventEmitter`.

An extremely popular way to _daemonize_ (never demonize, which means to "portray as wicked and threatening") a program is to use the [forever](https://npmjs.org/package/forever) module.  It can be used as a command-line script or as a module, and is built on some modules that are useful for creating Node daemons, like [forever-monitor](https://npmjs.org/package/forever-monitor) and [winston](https://npmjs.org/package/winston).

However, what I'm really interested in is the architecture of modules that provide services rather than utility modules for managing daemons.  One such example is [statsd](https://npmjs.org/package/statsd) from Etsy.  It's a network daemon for collecting statistics.  The core server code, [stats.js](https://github.com/etsy/statsd/blob/953063a2c6008480a5b4a4f7c8a814006f50bfc5/stats.js), uses `net.createServer` and a `switch` statement to execute commands based on the server's protocol.  Notable uses of `EventEmitter` include `backendEvents` for asynchronously communicating with the data storage layer, and automatic configuration file reloading.  I particularly like the fact the configuration file is reloaded -- it's a good use of Node's built-in features.

James Halliday's [smtp-protocol](https://npmjs.org/package/smtp-protocol) can be used to _implement_ SMTP servers (it isn't itself an SMTP server).  The server part of the module is based around a protocol parser, `ServerParser` -- a prototype class and a class for representing clients (`Client`).  Servers are created using `net.createServer`, much like the other projects I've already mentioned.

This module is useful because it demonstrates how to separate low-level implementation details from the high-level concerns of implementing a real production-ready server.  Completely different SMTP servers could be built using smtp-protocol as the foundation.  Real SMTP servers need to deal with things like relaying messages, logging, and managing settings, so James has separated that out whilst retaining a useful level of functionality for his module.

I've also been reading through the [telnet](https://npmjs.org/package/telnet) module, which like smtp-protocol can be used to implement a telnet server.

At the moment there seems to be a void between these reusable server modules and daemons that can be installed on production servers.  Node makes asynchronous I/O more accessible, which will lead to novel server implementations like Etsy's stats server.  If you've got an idea for a niche application layer server, then why not build it with Node?
