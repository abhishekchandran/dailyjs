---
layout: post
title: "Node Roundup: SocketCluster, i18n-generator, generator-gulp-angular"
author: "Alex Young"
categories:
- modules
- node
- internationalisation
- WebSocket
---

###SocketCluster

SocketCluster (GitHub: [TopCloud / socketcluster](https://github.com/topcloud/socketcluster), npm: [socketcluster](https://www.npmjs.org/package/socketcluster)) is a WebSocket server designed with clustering in mind.  The developers have tested for memory leaks and included benchmarks.  It handles client reconnection if a server crashes, and has a clustered memory store for temporary session data.

> SocketCluster lets you store session data using the socket.session object. This object gives you access to a cluster of in-memory stores called nData. You can effectively invoke any of the methods documented here to store and retrieve session data: <https://github.com/topcloud/ndata>

Basic usage looks like this:

{% highlight javascript %}
var SocketCluster = require('socketcluster').SocketCluster;

var socketCluster = new SocketCluster({
  workers: [9100, 9101, 9102],
  stores: [9001, 9002, 9003],
  balancerCount: 1,
  port: 8000,
  appName: 'myapp',
  workerController: 'worker.js',
  rebootWorkerOnError: false,
  addressSocketLimit: 50
});
{% endhighlight %}

The project is built with [iocluster](https://www.npmjs.org/package/iocluster) and [loadbalancer](https://www.npmjs.org/package/loadbalancer), by the same authors.

###i18n-generator

i18n-generator (GitHub: [huei90 / i18n-generator](https://github.com/huei90/i18n-generator), License: _MIT_, npm: [i18n-generator](https://www.npmjs.org/package/i18n-generator)) by Huei Tan is a library for converting i18n text files into JSON.

For example, given this input:

{% highlight text %}
i18n=> | en | zh_TW | de | my
you | you | 你 | Du | kamu
I | I | 我 | ich | Saya
love | love | 喜歡 | liebe | cinta
eat | eat | 吃 | essen | makan
ilovegithub | i love github | 我愛 Github | ich liebe Github | Saya cinta pada Github
{% endhighlight %}

It would generate this:

{% highlight javascript %}
{"you":"you","I":"I","love":"love","eat":"eat","ilovegithub":"i love github"}
{% endhighlight %}

for each language.  It comes with tests and browser support.

###generator-gulp-angular

I find it difficult to work on MVVM projects without some sort of build system so I can at least structure the project with CommonJS or AMD.  [generator-gulp-angular](https://github.com/Swiip/generator-gulp-angular) gives you a Yeoman generator that uses Gulp, Bowser, and AngularJS.

> This generator aims to takes the best from others generators like generator-angular, ngTailor and generator-gulp-webapp to offers the best workflow to start an application with AngularJS powered by Gulp!

> generator-gulp-angular scaffolds out an AngularJS application with a full featured gulpfile.js which offers all the tasks for modern web development.

It seems like a good way to get started with Gulp and AngularJS, which can actually be a little bit daunting.
