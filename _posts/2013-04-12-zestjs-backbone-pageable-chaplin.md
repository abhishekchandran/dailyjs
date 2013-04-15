---
layout: post
title: "ZestJS, backbone-pageable, Marionette and Chaplin"
author: "Alex Young"
categories: 
- frameworks
- libraries
- backbone.js
- mvc
---

###ZestJS

Øyvind Smestad sent in [ZestJS](http://zestjs.org/) (GitHub: [zestjs](https://github.com/zestjs), License: _Apache 2.0_), which offers an interesting take on client and server-side modularity:

> ZestJS provides client and server rendering for static and dynamic HTML widgets (Render Components) written as AMD modules providing low-level application modularity and portability.

It treats widgets as AMD components, with separate files for markup, JavaScript, and CSS.  It can then render the results on either the server or client.  The server-side renderer, [zest-server](https://github.com/zestjs/zest-server), is a small Node project that is capable of rendering views and serving static files.  It also handles routing, essentially mapping HTTP routes to what Zest calls "Render Components".

Some aspects of ZestJS remind me of Backbone.js -- the data loading can be performed on the initial page load, but remote APIs are easy to integrate as well.  It also uses `r.js` for building and optimizing single page web apps, which is similar to the workflow of many Backbone.js developers.

ZestJS was created by Guy Bedford, and there are [client](http://zestjs.org/#Install%20Zest%20Client) and [server](http://zestjs.org/#Install%20Zest%20Server) quick start guides.

###backbone-pageable

backbone-pageable (GitHub: [wyuenho / backbone-pageable](https://github.com/wyuenho/backbone-pageable), License: _MIT_) by Jimmy Yuen Ho Wong is a drop-in replacement for `Backbone.Collection` that adds support for server and client-side pagination.  It includes options for sorting, infinite paging, and caching:

> It comes with reasonable defaults and works well with existing server APIs. Besides being really good at pagination and sorting, it is also really smart as syncing changes across pages while paginating on the client-side. It is also extremely lightweight - only 4k minified and gzipped

It supports query parameters, so you can easily set up your pagination links with variables to meet your server's requirements (or perhaps to allow multiple pagination controls on a page).

{% highlight javascript %}
var Book = Backbone.Model.extend({});

var Books = Backbone.PageableCollection.extend({
  model: Book,
  url: 'api.mybookstore.com/books',

  state: {
    firstPage: 0,
    currentPage: 2,
    totalRecords: 200
  },

  queryParams: {
    currentPage: 'current_page',
    pageSize: 'page_size'
  }
});
{% endhighlight %}

The project comes with some serious test coverage, including a test suite geared up for Zepto which is a nice touch.

The author is currently working on releasing a new version that adds Backbone 1.0 support.  It should be 1.2.2, so keep a lookout for that if you're already on Backbone 1.0.

###Comparison of Marionette and Chaplin

Mathias Schäfer, who is one of the creators of [Chaplin.js](http://chaplinjs.org/), sent in a comparison of [Marionette and Chaplin](http://9elements.com/io/index.php/comparison-of-marionette-and-chaplin/).  Both libraries attempt to address various limitations of Backbone.js -- Chaplin.js adds better support for CoffeeScript class hierarchies, stricter memory management, lazy-loading modules, and publish/subscribe for cross-module communication.

The comparison is detailed and reveals some of the thinking that went into Chaplin.js in the first place:

> Compared to Marionette, Chaplin acts more like a framework. It's more opinionated and has stronger conventions in several areas. It took ideas from server-side MVC frameworks like Ruby on Rails which follow the convention over configuration principle. The goal of Chaplin is to provide well-proven guidelines and a convenient developing environment.

The post already has interesting comments -- Mathias seems to be following up questions with some well thought out responses.
