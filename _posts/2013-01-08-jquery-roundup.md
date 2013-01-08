---
layout: post
title: "jQuery Roundup: ParamQuery Grid, Backbone.ViewDSL, Events Demo"
author: Alex Young
categories:
- jquery
- plugins
- backbone.js
---

<div class="intro">
Note: You can send your plugins and articles in for review through our <a href="/contact.html">contact form</a> or <a href="http://twitter.com/dailyjs">@dailyjs</a>.
</div>

###ParamQuery Grid

![ParamQuery](/images/posts/paramquery.png)

[ParamQuery Grid](http://paramquery.com/) (GitHub: [paramquery / grid](https://github.com/paramquery/grid), License: _MIT_) by Paramvir Dhindsa is a table grid plugin that's based on jQuery UI widgets.  It supports sorting, row and cell selection, built-in and custom editing, resizing, and pagination.

The author has written [full API documentation for ParamQuery](http://paramquery.com/api), and [an introductory tutorial](http://paramquery.com/tutorial).  Additional data formats can be supported with the [dataModel API](http://paramquery.com/api#option-dataModel), but it works with XML and JSON out of the box.

###Backbone.ViewDSL

[Backbone.ViewDSL](http://andreypopp.github.com/backbone.viewdsl/) (GitHub: [andreypopp / backbone.viewdsl](https://github.com/andreypopp/backbone.viewdsl), License: _BSD3_) by Andrey Popp is a DSL for defining `Backbone.View` hierarchies.  Views can be automatically loaded (AMD is supported), instantiated, and interpolated.

The author's example compares a ViewDSL class with a standard Backbone class:

{% highlight coffeescript %}
class App extends Backbone.ViewDSL.View
  template: """
    <h1>{{options.title}}</h1>
    <view name="app.views.Sidebar" id="sidebar" />
    <view name="app.views.Content" id="content" />
    <div class="footer">{{options.title}} by {{options.author}}</div>
    """
{% endhighlight %}

In that example, `app.views.Sidebar` refers to another `Backbone.View`.  A `view` attribute is also supported, and views can be accessed with `Backbone.ViewDSL.View.from`.  Although Andrey describes the library as 'tiny', it packs in other features including conditional DOM removal, and there are some [PhantomJS-powered Mocha tests](http://metaskills.net/mocha-phantomjs/) as well.

###Events Demo

[Events Demo](http://liouh.com/jsevents/) (GitHub: [liouh / js-events-demo](https://github.com/liouh/js-events-demo)) by Henry Liou is an interactive demo that shows how each property works on the event object jQuery passes to `.on`.  It uses nested elements so you can see how `target` and `relatedTarget` change depending on which element the event was triggered on.

Given how many people confuse the target properties, it made me wonder if this would be better than the [official jQuery documentation](http://api.jquery.com/category/events/event-object/).  This project was sent in by Anthony Ettinger.

