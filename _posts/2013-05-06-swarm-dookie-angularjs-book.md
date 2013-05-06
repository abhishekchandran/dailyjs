---
layout: post
title: "Swarm, Dookie, AngularJS Book"
author: "Alex Young"
categories: 
- node
- modules
- books
- css
---

###Swarm

[Swarm](http://ppyr.us/swarm/test/grid.html) (GitHub: [gritzko / swarm](https://github.com/gritzko/swarm), License: _MIT_) by Victor Grishchenko is a data synchronisation library that can synchronise objects on clients and servers.

> Swarm is built around its concise four-method interface that expresses the core function of the library: synchronizing distributed object replicas. The interface is essentially a combination of two well recognized conventions, namely get/set and on/off method pairs, also available as getField/setField and addListener/removeListener calls respectively.

{% highlight javascript %}
var obj = swarmPeer.on(id, callbackFn); // also addListener()
obj.set('field',value);
obj.getField()===obj.get('field')===obj.field;
obj.on('field', fieldCallbackFn);
obj.off('field', fieldCallbackFn);
swarmPeer.off(id, callbackFn);  // also removeListener()
{% endhighlight %}

The author has defined an addressing protocol that uses tokens to describe various aspects of an event and object.  For more details, see [Swarm: specifying events](https://github.com/gritzko/swarm/blob/master/doc/Specifiers.md).

###Dookie

[Dookie](http://labs.voronianski.com/dookie-css/) (GitHub: [voronianski / dookie-css](https://github.com/voronianski/dookie-css), License: _MIT_, npm: [dookie-css](https://npmjs.org/package/dookie-css)) by Dmitri Voronianski is a CSS library that's built on [Stylus](https://github.com/learnboost/stylus).  It provides several useful mixins and components:

* Reset mixins: `reset()`, [normalize()](https://github.com/necolas/normalize.css/), and `fields-reset()`
* Helpers: Shortcuts for working with `display`, fonts, images and high pixel ratio images
* Sprites
* Vendor prefixes
* Easings and gradients

Dmitri has also included Mocha/PhantomJS tests for checking the generated output and visualising it.

###Developing an AngularJS Edge

[Developing an AngularJS Edge](http://bleedingedgepress.com/our-books/developing-an-angularjs-edge/) by Christopher Hiller is a new book about AngularJS aimed at existing JavaScript developers who just want to learn AngularJS.  The author has posted examples on GitHub here: [angularjsedge / examples](https://github.com/angularjsedge/examples), and there's a [sample chapter](http://www.bleedingedgepress.com/downloads/developing-an-angularjs-edge-sample-chapter.epub) (ePub).

The book is being sold through Gumroad for $14.95, reduced from $19.95.  The author notes that it is also available through Amazon and Safari Books Online.

