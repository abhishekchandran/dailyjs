---
layout: post
title: "P, EasyWebWorker, OpenPGP.js"
author: "Alex Young"
categories: 
- node
- modules
- crypto
- p2p
- webworkers
---

###P

[P](http://ozan.io/p/) (GitHub: [oztu / p](https://github.com/oztu/p), License: _Apache 2_, npm: [onramp](https://npmjs.org/package/onramp), bower: _p_) by Ozan Turgut is a client-side library with a WebSocket server for creating P2P networks by allowing browser-to-browser connections.

The _onramp_ Node module is used to establish connections, but after that it isn't necessary for communication between clients.  The author has written up documentation with diagrams to explain how it works.  Like other similar projects, the underlying technology is [WebRTC](http://www.webrtc.org/), so it only works in Chrome or Firefox Nightly.

###EasyWebWorker

[EasyWebWorker](http://easywebworker.com/) (GitHub: [ramesaliyev / EasyWebWorker](https://github.com/ramesaliyev/EasyWebWorker), License: _MIT_) by Rameş Aliyev is a wrapper for web workers which allows functions to be executed directly, and can execute global functions in the worker.

A fallback is provided for older browsers:

{% highlight coffeescript %}
# Create web worker fallback if browser doesnt support Web Workers.
if this.document isnt undefined and !window.Worker and !window._WorkerPrepared
  window.Worker = _WorkerFallback
{% endhighlight %}

The `_WorkerFallback` class is provided, and uses `XMLHttpRequest` or `ActiveXObject`.

The source code is nicely commented if you want to look at what it does in more detail: [easy-web-worker.coffee](https://github.com/ramesaliyev/EasyWebWorker/blob/master/easy-web-worker.coffee).

###OpenPGP.js

Jeremy Darling sent in [OpenPGP.js](http://openpgpjs.org/) (GitHub: [openpgpjs / openpgpjs](https://github.com/openpgpjs/openpgpjs), License: _LGPL_), which is an [OpenPGP](http://www.openpgp.org/) implementation for JavaScript:

> This is a JavaScript implementation of OpenPGP with the ability to generate public and private keys.  Key generation can be a bit slow but you can also import your own keys.

Jeremy found that OpenPGP.js is used by [Mailvelope](http://www.mailvelope.com/), which is a browser extension that brings OpenPGP to webmail services like Gmail.  That means Mailvelope can encrypt messages without having to upload a private key to a server.
