---
layout: post
title: "Backbone Fetch Cache, Backbone.VirtualCollection, WTCSS"
author: Alex Young
categories:
- backbone.js
- plugins
---

###Backbone Fetch Cache

Backbone Fetch Cache (GitHub: [mrappleton / backbone-fetch-cache](https://github.com/mrappleton/backbone-fetch-cache)) by Andy Appleton caches Backbone's collection and model fetch requests.  Data is stored in `localStorage` to speed up rendering.  This is useful for caching Ajax requests with APIs that don't allow control over response cache headers.

The plugin supports preloading data with the `prefill` option which can be passed to `fetch`, and the author has included some Jasmine tests.

###Backbone.VirtualCollection

Backbone.VirtualCollection (GitHub: [p3drosola / Backbone.VirtualCollection](https://github.com/p3drosola/Backbone.VirtualCollection), License: _MIT_, npm: [backbone-virtual-collection](https://npmjs.org/package/backbone-virtual-collection)) by Pedro Solá allows Backbone.Marionette's [CollectionViews](https://github.com/marionettejs/backbone.marionette/blob/master/docs/marionette.collectionview.md) and [CompositeViews](https://github.com/marionettejs/backbone.marionette/blob/master/docs/marionette.compositeview.md) to be used with instances of `Backbone.Collection`.  This allows collections to be projected and sorted.

This example is from the project's documentation:

{% highlight javascript %}
var virtual_collection = new Backbone.VirtualCollection(tasks_collection, function (task) {
  return task.get('user_id') == 13;
});

var view = new TaskListView({
  collection: virtual_collection
});
{% endhighlight %}

The project has Mocha tests and some details on its philosophy in the readme.

###WTCSS

![WTCSS](/images/posts/wtcss.png)

[WTCSS](http://css.benjaminbenben.com/) (GitHub: [benfoxall / wtcss](https://github.com/benfoxall/wtcss), License: _MIT_) by Ben Foxall uses PhantomJS to analyse the CSS on a page, then attempts to visually indicate where each rule applies to using a Canvas overlay.

It looks impressive -- there are demos on the project's homepage, and I suspect it could form the basis for a more advanced CSS analysis and debugging tool.
