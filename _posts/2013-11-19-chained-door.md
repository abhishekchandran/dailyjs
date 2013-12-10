---
layout: post
title: "Chained, Door"
author: Alex Young
categories:
- jquery
- es6
- components
- libraries
---

###Chained

[Chained](http://www.vittoriozaccaria.net/chained/) (GitHub: [vzaccaria / chained](https://github.com/vzaccaria/chained), License: _MIT_) is another ES6 experiment.  It allows APIs that return promises to be mixed with functions that take parameters and return mutated objects.  In Vittorio's example he mixes jQuery's network methods with Underscore.js to download JSON and then filter it:

{% highlight coffeescript %}
getUser = (user) ->
  _("https://npmjs.org/~#{user}")
    .get()
    .extractLinks()
    .filter(-> /package/.test(arguments[0]))
    .map(-> "https://npmjs.org#{arguments[0]}")
    .log()

getUser("vzaccaria")
{% endhighlight %}

In this CoffeeScript example, methods that use promises (`get`) are mixed with functions that take objects as the first argument (`filter`, `map`), using a consistent chainable API.  To make this work, Vittorio has used ES6's introspection features.

The project has detailed notes in the readme about how this works.  He mentions that the library came about after trying to create DSLs with JavaScript.

###Door

Olivier Wietrich sent in [Doors](http://bredele.github.io/doors/) (GitHub: [bredele / doors](https://github.com/bredele/doors), License: _MIT_, component: _bredele/doors_), a module for conditionally restricting access to `open` events that are triggered when all locks are unlocked.

> \[State machines and promises\] both have something missing. A transition occurs when one condition is triggered. Things are not so simple in real life. You will probably have more than one condition to do something, but one condition is sufficient to not do it. Think about a door with multiple locks: you can't open the door until all locks are unlocked.

Looking at the documentation, it seems like the author wants to use it to restrict access to an API until certain authentication preconditions are met.  There's a simple HTML example that uses a graphical door, and two locks.  You can toggle locks and add more.

