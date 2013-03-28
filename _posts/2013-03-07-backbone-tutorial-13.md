---
layout: post
title: "Backbone.js Tutorial: Routes"
author: Alex Young
categories: 
- backbone.js
- mvc
- node
- backgoog
---

<ul class="parts">
  <li><a href="http://dailyjs.com/2012/11/29/backbone-tutorial-1/">Part 1: Build Environment</a></li>
  <li><a href="http://dailyjs.com/2012/12/06/backbone-tutorial-2/">Part 2: Google's APIs and RequireJS</a></li>
  <li><a href="http://dailyjs.com/2012/12/13/backbone-tutorial-3/">Part 3: Authenticating with OAuth2</a></li>
  <li><a href="http://dailyjs.com/2012/12/20/backbone-tutorial-4/">Part 4: Backbone.sync</a></li>
  <li><a href="http://dailyjs.com/2012/12/27/backbone-tutorial-5/">Part 5: List Views</a></li>
  <li><a href="http://dailyjs.com/2013/01/03/backbone-tutorial-6/">Part 6: Creating Lists</a></li>
  <li><a href="http://dailyjs.com/2013/01/10/backbone-tutorial-7/">Part 7: Editing Lists</a></li>
  <li><a href="http://dailyjs.com/2013/01/17/backbone-tutorial-8/">Part 8: Deleting Lists</a></li>
  <li><a href="http://dailyjs.com/2013/01/24/backbone-tutorial-9/">Part 9: Tasks</a></li>
  <li><a href="http://dailyjs.com/2013/01/31/backbone-tutorial-10/">Part 10: Oh No Not More Tasks</a></li>
  <li><a href="http://dailyjs.com/2013/02/07/backbone-tutorial-11/">Part 11: Spies, Stubs, and Mocks</a></li>
  <li><a href="http://dailyjs.com/2013/02/14/backbone-tutorial-12/">Part 12: Testing with Mocks</a></li>
  <li><a href="http://dailyjs.com/2013/03/07/backbone-tutorial-13/"><strong>Part 13: Routes</strong></a></li>
  <li><a href="http://dailyjs.com/2013/03/14/backbone-tutorial-14/">Part 14: Customosing the UI</a></li>
  <li><a href="http://dailyjs.com/2013/03/28/backbone-tutorial-15/">Part 15: Updates for 1.0, Clear Complete</a></li>
</ul>

###Preparation

Before starting this tutorial, you'll need the following:

* [alexyoung / dailyjs-backbone-tutorial](https://github.com/alexyoung/dailyjs-backbone-tutorial) at commit `0c6de32`
* The API key from part 2
* The "Client ID" key from part 2
* Update `app/js/config.js` with your keys (if you've checked out my source)

To check out the source, run the following commands (or use a suitable Git GUI tool):

{% highlight text %}
git clone git@github.com:alexyoung/dailyjs-backbone-tutorial.git
cd dailyjs-backbone-tutorial
git reset --hard 0c6de32
{% endhighlight %}

###Routes

So far we've implemented basic list and task management, but working with multiple lists is tricky because lists can't be referenced by the URL.  If the page is reloaded, the current list isn't remembered, and lists can't be bookmarked.

Fortunately, Backbone provides a solution for both of these issues: `Backbone.Router`.  This provides a neat wrapper around hash URLs and `history.pushState`.

###When to Use Hash URLs

I'll admit I find hash URLs annoying, and this sentiment seems to have been perpetuated by Twitter's implementation of them.  However, there is a good side to hash URLs: they require less work to build and are backwards compatible with older browsers.

Using `history.pushState` means the browser can potentially display any URL you want.  Rather than `/#lists/id`, the prettier `/lists/id` can be displayed.  However, without a suitable server-side setup, visiting `/lists/id` before the main application has loaded will fail while the hash URL version will work.

If you're making a fairly simple and self-contained single page application, then you may wish to avoid `pushState` and use hash URLs instead.

Either way, Backbone makes it easy to switch between both schemes.  Hash URLs are the default, and `history.pushState` will be used when specified with `Backbone.history.start({ pushState: true })`.

###The Routes File

It's generally a good idea to keep routes separate from the rest of the application.  Create a new file called `app/js/routes.js` and `extend` Backbone's router:

{% highlight javascript %}
define(function() {
  return Backbone.Router.extend({
    routes: {
      'lists/:id': 'openList'
    },

    initialize: function() {
    },

    openList: function(id) {
    }
  });
});
{% endhighlight %}

This code defines the route.  This application will just need one for now: `lists/:id`.  The `:id` part is a parameter, which will be extracted by `Backbone.Router` and sent as an argument to `openList`.

###Load the Router

The centralised `App` class is as good a place as any to load the routes and set them up.  Open `app/js/app.js` and change `define` to include `'routes'`:

{% highlight javascript %}
define([
  'gapi'
, 'routes'
, 'views/app'
, 'views/auth'
, 'views/lists/menu'
, 'collections/tasklists'
, 'collections/tasks'
],

function(ApiManager, Routes, AppView, AuthView, ListMenuView, TaskLists, Tasks) {
  var App = function() {
    this.routes = new Routes();
{% endhighlight %}

Now, move down to around line 35 where there's a callback that runs when the API manager is ready.  This is where `Backbone.history.start` should be called:

{% highlight javascript %}
App.prototype = {
  views: {},
  collections: {},
  connectGapi: function() {
    var self = this;
    this.apiManager = new ApiManager(this);
    this.apiManager.on('ready', function() {
      self.collections.lists.fetch({ data: { userId: '@me' }, success: function(collection, res, req) {
        self.views.listMenu.render();
        Backbone.history.start();
      }});
    });
  }
};
{% endhighlight %}

It's technically safe to call this when the routes have been loaded, but the `openList` route handler requires that some lists exist, so it's better to load it when the API is ready.

The purpose of the `start` method is to begin monitoring `hashchange` events -- whenever the browser address bar's URL changes the router will be invoked.

###Opening Lists Using Events

To write decoupled Backbone applications, you need to think in terms of the full Backbone stack: models and collections, and views.  When someone visits a list URL from a bookmark that refers to a specific model, the route handler should be able to find the associated model.

Backbone's documentation is quite clear about the power of custom events, and that's basically how `openList` in `app/js/routes.js` should work:

{% highlight javascript %}
openList: function(id) {
  if (bTask.collections.lists && bTask.collections.lists.length) {
    var list = bTask.collections.lists.get(id);
    if (list) {
      list.trigger('select');
    } else {
      console.error('List not found:', id);
    }
  }
}
{% endhighlight %}

I've been strict about checking for the existence of the `lists` collection, and even when fetching a given `list` model from the collection.  The main reason for this was to be able to show sensible error messages, but for now there's just a `console.error` to help track issues loading data.

The final piece of the puzzle is the view code that has the responsibility of opening lists.  Open `app/js/views/lists/menuitem.js` and make the following changes:

1. Add `this.model.on('select', this.open, this);` to the `initialize` method
2. Add `bTask.routes.navigate('lists/' + this.model.get('id'));` to the `render` method

The first line binds the custom event, `select`, from the view's model (which represents the list).  The second line causes the browser's URL to be updated -- you'll find yourself using `routes.navigate` quite a lot in more complicated applications.

###Summary

Combining events and routes is the secret to writing decoupled Backbone applications.  It can be difficult to do this well -- there are definitely often lazy solutions that can result in a little bit too much spaghetti code.  To avoid situations like this, think in terms of models, collections, views, and their relationships.

The full source for this tutorial can be found in [alexyoung / dailyjs-backbone-tutorial, commit 85c358](https://github.com/alexyoung/dailyjs-backbone-tutorial/commit/85c35852a2c4e820a9e6e855c30ec83124f8a7f5).

