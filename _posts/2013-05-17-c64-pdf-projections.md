---
layout: post
title: "Impossible Mission, Full-Text Indexing, Backbone.Projections"
author: "Alex Young"
categories: 
- games
- backbone.js
- node
- pdf
---

###Impossible Mission

![Impossible Mission](/images/posts/c64-impossible-mission.png)

[Impossible Mission](http://impossible-mission.krissz.hu/) by Krisztián Tóth is a JavaScript remake of the C64 classic.  You can view the source to see how it all works, if things like `this.dieByZapFrames` and `this.searchedFurniture` sound appealing to you.

Krisztián previously sent in [Boulder Dash and Wizard of Wor](http://dailyjs.com/2012/04/06/toth-xregexp-plastron/) which were similar remakes written using the same approach.

###Client-Side Full-Text Indexing

Gary Sieling sent in a post he wrote about full-text indexing with client-side JavaScript, in which he looks at PDF.js and Lunr: [Building a Full-Text Index in JavaScript](http://garysieling.com/blog/building-a-full-text-index-in-javascript).  I [briefly mentioned Lunr](http://dailyjs.com/2013/03/01/localstorage-lunr-vlug/) by Oliver Nightingale back in March.

> One great thing about this type of index is that the work can be done in parallel and then combined as a map-reduce job. Only three entries from the above object need to be combined, as "fields" and "pipeline" are static.

###Backbone.Projections

In relational databases, a projection is a subset of available data.  [Backbone.Projections](http://andreypopp.com/posts/2013-05-15-projections-for-backbone-collections.html) (GitHub: [andreypopp / backbone.projections](https://github.com/andreypopp/backbone.projections), License: _MIT_, npm: [backbone.projections](https://npmjs.org/package/backbone.projections)) by Andrey Popp is the equivalent for Backbone collections -- they allow a transformed subset of values in a collection can be represented and synced.

The supported projections are `Capped` and `Filtered`.  Capped collections are limited based on a size and function -- the function will be used to order the results prior to truncating them.  Filtered projections filter out results based on a function that returns a boolean.

Projections can be composed by passing one project to another.  This example creates a `Filtered` projection, and then passes it to a `Capped` projection to limit and order the results:

{% highlight javascript %}
var todaysPosts = new Filtered(posts, {
  filter: function(post) {
    return post.get('date').isToday();
  }
});

var topTodaysPosts = new Capped(todaysPosts, {
  cap: 5,
  comparator: function(post) {
    return post.get('likes');
  }
});
{% endhighlight %}

The author has written unit tests with Mocha, and documentation is available in the readme.
