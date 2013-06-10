---
layout: post
title: "Easystar.js, Boolasync, Synchroscope"
author: "Alex Young"
categories: 
- angularjs
- libraries
- node
- async
---

###Easystar.js

![easystar](/images/posts/easystarjs.png)

[Easystar.js](http://easystar.nodejitsu.com/demo.html) (GitHub: [prettymuchbryce / easystarjs](https://github.com/prettymuchbryce/easystarjs), License: _MIT_) by Bryce Neal is an [A* pathfinding API](http://en.wikipedia.org/wiki/A*_search_algorithm).  Given a map of tiles, easystar will find a path through traversable tiles on the grid:

{% highlight javascript %}
var easystar = new EasyStar.js();
var grid = [[0,0,1,0,0],
            [0,0,1,0,0],
            [0,0,1,0,0],
            [0,0,1,0,0],
            [0,0,0,0,0]];

easystar.setGrid(grid);
easystar.setAcceptableTiles([0]);

easystar.findPath(0, 0, 4, 0, function(path)) {
  if (path === null) {
    console.log('Path was not found.');
  } else {
    console.log('Path was found. The first Point is:', path[0]);
  }
});

easystar.setIterationsPerCalculation(1000); 
easystar.calculate()
{% endhighlight %}

The readme has a full breakdown of the methods used in this example, and installation instructions.

###Boolasync

Boolasync (GitHub: [olalonde / boolasync](https://github.com/olalonde/boolasync), License: _MIT_, npm: [boolasync](https://npmjs.org/package/boolasync)) by Olivier Lalonde is a module for composing logic using chained calls to asynchronous functions:

{% highlight javascript %}
fn1.and(fn2).or(fn3).and(fn4.orNot(fn5).and(fn6)).eval(function(err, res) {
  if (err) return console.error(err);
  if (res) {
    console.log('The expression evaluated to true.');
  } else {
    console.log('The expression evaluated to false.');
  }
});
{% endhighlight %}

It supports optional "monkey patching" which adds boolean logic methods to `Function.prototype`.  Olivier has included Mocha tests and a roadmap for future features.

###synchroscope

synchroscope (GitHub: [dtinth / synchroscope](https://github.com/dtinth/synchroscope), License: _MIT_, npm: [synchroscope](https://npmjs.org/package/synchroscope)) by Thai Pangsakulyanont allows the scope to be shared between multiple AngularJS clients.  It works by sending data encoded using `JSON.stringify` over Socket.IO.

There's a [synchroscope instance running on Nodejitsu](https://synchroscope.jit.su/) so you can try out examples using jsFiddle and similar services.  The author has asked Nodejitsu for an open source drone but is currently waiting for a response.  He's got two demos running: [AngularJS Todos](http://jsfiddle.net/thai/MxNJM/) and [Tic Tac Toe Game](http://jsfiddle.net/thai/8Gsyr/).

The bundled server stores everything in-memory, so it doesn't currently scale across multiple processes.  I imagine the server could easily be modified to use a database or perhaps pub/sub.

On the client the API is surprisingly minimal -- once the `$ync` dependency has been added, data can be shared from `$scope` by calling `$ync($scope, keys, room)`.  It seems like an idiomatic way to make real-time web applications with AngularJS.

