---
layout: post
title: "Orientation and Vibration APIs, Mongomery"
author: Alex Young
categories:
- node
- modules
- npm
- libraires
- mongo
- mobile
- generators
---

###Orientation and Vibration APIs for Games

Andrzej Mazur sent in an article about using the [orientation and vibration APIs for game development](https://hacks.mozilla.org/2015/04/mobile-game-development-with-the-device-orientation-and-vibration-apis/):

> The Device Orientation API specification is still in the Working Draft status, so there might be some code-breaking changes introduced in the future. It's an experimental technology and should be treated as such. All implementations are still missing the compassneedscalibration event. Also, there are differences in browser implementations which should be taken into consideration. For instance, Chrome and Opera don't support the devicemotion event.
>
> The Vibration API is another feature that can boost the mobile experience. Most devices support it (except iOS Safari and Opera Mini), and it works great on Firefox OS devices.

I've never used the vibration API, but apparently you can access it with `window.navigator.vibrate`.  It even supports an array of values for vibrating multiple times.  Andrzej's argument is that you can use these APIs to differentiate your game from other mobile web games, and while this is true it'll take a fair bit of experimentation to get orientation-based controls working well!

###Mongomery

Coderaiser has sent in a few generator-based modules recently, but I missed Mongomery (GitHub: [coderaiser/node-mongomery](https://github.com/coderaiser/node-mongomery), License: _MIT_, npm: [mongomery](https://www.npmjs.com/package/mongomery)), a module that uses generators for MongoDB.  It uses [ruff](https://github.com/coderaiser/ruff), which was Coderaiser's module for giving generators a more `EventEmitter`-inspired API:

{% highlight javascript %}
var mongomery = require('mongomery');

mongomery(function*(mongo) {
  var url = 'mongodb://localhost:27017/myproject',
  var db = yield mongo.connect(url),
  var collection = db.collection('mongolog'),
  var docs = yield collection.find({}).toArray();

  docs.forEach(function(item) {
    console.log(item);
  });

  db.close();
}).on('error', function(error) {
  console.log(error.message);
});
{% endhighlight %}

It'll take us a few years to really understand how new features like generators should be used in terms of databases, but I'm very interested in using generator syntax for databases.

An alternative that I've enjoyed experimenting with is [Mongorito](http://mongorito.com/), which is more of an ODM-style API.  The syntax is more succinct than Mongoose, while still remaining familiar.
