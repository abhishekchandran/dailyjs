---
layout: post
title: "jQuery Roundup: 1.9.1, jui_datagrid, jQuery Waiting, jquery.defer"
author: Alex Young
categories:
- jquery
- plugins
- animations
- database
- backbone.js
---

<div class="intro">
Note: You can send your plugins and articles in for review through our <a href="/contact.html">contact form</a>.
</div>

###jQuery 1.9.1

[jQuery 1.9.1](http://blog.jquery.com/2013/02/04/jquery-1-9-1-released/) has been released:

> Whether you're using 1.9.0 or using an older version, these are the droids you're looking for.

There are bug fixes for Chrome, IE, and Safari, and a few small enhancements like [#13150: Be able to determine if $.Callback() has functions](http://bugs.jquery.com/ticket/13150).

###jui_datagrid

![jui_datagrid](/images/posts/jui_datagrid.png)

[jui_datagrid](http://www.pontikis.net/labs/jui_datagrid/) (GitHub: [pontikis / jui_datagrid](https://github.com/pontikis/jui_datagrid), License: _MIT_) by Christos Pontikis is a one of those "rich table" plugins that makes tabular data sortable, editable, and so on.  It has a specific focus on editing server-side data, and will work with JSON data out of the box.  It supports multiple instances on the same page, jQuery UI themes, localisation, and a modular design that makes adding new data filters easier.

There is a [a demo of jui_datagrid](http://www.pontikis.net/labs/jui_datagrid/demo/) that shows the major features.

###jQuery Waiting

[jQuery Waiting](http://trentrichardson.com/examples/jQuery-Waiting/) (GitHub: [trentrichardson / jQuery-Waiting](https://github.com/trentrichardson/jQuery-Waiting), License: _MIT/GPL_) by Trent Richardson is a plugin for displaying spinners that's designed to be cross-browser.  Instead of relying on modern CSS animations, it simply switches CSS classes on sets of elements.  It has a namespaced event-based API, so you can see when the control is enabled, starts playing, and so on:

{% highlight javascript %}
// Initialise
$el.waiting({});

// Play
$el.waiting('play');

// Event example
$el.bind('play.waiting', function(e){});
{% endhighlight %}

###jquery.defer

jquery.defer/jquery.undefer (GitHub: [wheresrhys / jquery.defer](https://github.com/wheresrhys/jquery.defer), License: _MIT_) by Rhys Evans are a pair of utility methods for making an object's methods wait until a deferred object has resolved.  The example Rhys provides of this in action is lazy loading Google Maps:

{% highlight javascript %}
$.defer(GoogleMaps.prototype, _mapsLoaded, {exclude: 'init'});
{% endhighlight %}

Rhys also sent in Backbone Namespaced Events (GitHub: [wheresrhys / backbone.namespaced-events](https://github.com/wheresrhys/backbone.namespaced-events), License: _MIT_), which uses the syntax of [namespaced events](http://docs.jquery.com/Namespaced_Events) for Backbone's custom events implementation.  To use namespaced events, call `Backbone.extend(obj, Backbone.NamespacedEvents)` on a Backbone object instance.  Alternatively, `Backbone.NamespacedEvents.overwriteNativeEvents()` can be called to use it everywhere.

