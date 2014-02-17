---
layout: post
title: "Backbone.React.Component, backbone-dom-view"
author: Alex Young
categories:
- backbone
- dom
- views
- react
---

###Backbone.React.Component

If you like Facebook's React library and Backbone.js, then take a look at José Magalhães' Backbone.React.Component (GitHub: [magalhas / backbone-react-component](https://github.com/magalhas/backbone-react-component), License: _MIT_, Bower: _backbone-react-component_).  It acts as a bridge so you can bind models, collections, and components on both the client and server.

The author has made a [blog example](https://github.com/magalhas/backbone-react-component/tree/master/examples/blog) that you can run locally.  The server uses Express, and keeps collections updated with data both on the server and in the browser.

###backbone-dom-view

backbone-dom-view (GitHub: [redexp / backbone-dom-view](https://github.com/redexp/backbone-dom-view), License: _MIT_, Bower: _backbone-dom-view_) by Sergii Kliuchnyk is a view class for Backbone that allows selectors to be bound to helper methods using a shorthand notation that supports binding model fields, view events, and calculations.

Sergii's example is a to-do model:

{% highlight coffeescript %}
View = Backbone.DOMView.extend
  template:
    '.title':
      html: '@title'
    '.state':
      class:
        'done': '@is_done'
{% endhighlight %}

It has RequireJS support, tests, and documentation in the readme.
