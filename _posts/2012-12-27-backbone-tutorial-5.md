---
layout: post
title: "Backbone.js Tutorial: List Views"
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
  <li><a href="http://dailyjs.com/2012/12/27/backbone-tutorial-5/"><strong>Part 5: List Views</strong></a></li>
  <li><a href="http://dailyjs.com/2013/01/03/backbone-tutorial-6/">Part 6: Creating Lists</a></li>
  <li><a href="http://dailyjs.com/2013/01/10/backbone-tutorial-7/">Part 7: Editing Lists</a></li>
  <li><a href="http://dailyjs.com/2013/01/17/backbone-tutorial-8/">Part 8: Deleting Lists</a></li>
  <li><a href="http://dailyjs.com/2013/01/24/backbone-tutorial-9/">Part 9: Tasks</a></li>
  <li><a href="http://dailyjs.com/2013/01/31/backbone-tutorial-10/">Part 10: Oh No Not More Tasks</a></li>
  <li><a href="http://dailyjs.com/2013/02/07/backbone-tutorial-11/">Part 11: Spies, Stubs, and Mocks</a></li>
</ul>

###Preparation

Before starting this tutorial, you'll need the following:

* [alexyoung / dailyjs-backbone-tutorial](https://github.com/alexyoung/dailyjs-backbone-tutorial) at commit `fcd653ec6`
* The API key from part 2
* The "Client ID" key from part 2
* Update `app/js/config.js` with your keys (if you've checked out my source)

To check out the source, run the following commands (or use a suitable Git GUI tool):

{% highlight text %}
git clone git@github.com:alexyoung/dailyjs-backbone-tutorial.git
cd dailyjs-backbone-tutorial
git reset --hard fcd653ec6
{% endhighlight %}

###Wireframe

The application we're building has several main interface elements:

* A two column layout for displaying task lists and tasks
* Forms for adding and editing each item type
* Buttons for invoking the forms, deleting items, and clearing complete items
* Task state control (done checkbox)

The image below shows the basic layout.

<div class="image">
  <img src="/images/posts/backbone-tutorial-wireframe.jpg" alt="" />
  <small>The application's wireframe.</small>
</div>

In this tutorial we'll start implementing the interface by using an unordered list to represent task lists.

###List Items

Despite being relatively simple, implementing a navigable list of task lists involves several Backbone.js elements:

* HTML templates
* Backbone views: `ListMenuView`, `ListMenuItemView`
* Backbone collection: `TaskLists`

The `ListMenuView` contains the task list menu, and the `ListMenuItemView` is the navigation item for each task list itself.  This can be modeled as a `ul` and a set of `li` elements.

Create a new directory called `app/js/views/lists` to store the task list-related `Backbone.View` classes, and another called `app/js/templates/lists` for the corresponding templates.

###View: `ListMenuView`

This view resides in `app/js/views/lists/menu.js`:

{% highlight javascript %}
define(['views/lists/menuitem'], function(ListMenuItemView) {
  var ListMenuView = Backbone.View.extend({
    el: '.left-nav',
    tagName: 'ul',
    className: 'nav nav-list lists-nav',

    events: {
    },

    initialize: function() {
      this.collection.on('add', this.render, this);
    },

    render: function() {
      // TODO
    }
  });

  return ListMenuView;
});
{% endhighlight %}

It loads `views/lists/menuitem` which we'll create in a moment.  Then it binds itself to the `.left-nav` element which was created by `AppView` and its corresponding template.  The menu itself is an unordered list, and it uses some class names that will become more relevant once styles are added.

Notice that this view expects a collection.  Collections can be passed to views during instantiation.  For example, `new ListMenuView({ collection: lists })` will pass the `lists` collection to an instance of this view.

The `render` method should look like this:

{% highlight javascript %}
render: function() {
  var $el = $(this.el)
    , self = this;

  this.collection.each(function(list) {
    var item, sidebarItem;
    item = new ListMenuItemView({ model: list });
    $el.append(item.render().el);
  });

  return this;
}
{% endhighlight %}

The view's element is used as the container for each `ListMenuItemView` which is passed a model by iterating over the collection.

###View: `ListMenuItemView`

The `app/js/views/lists/menuitem.js` is similar to the previous view, but makes use of a template and Backbone's declarative event binding feature.

{% highlight javascript %}
define(['text!templates/lists/menuitem.html'], function(template) {
  var ListMenuItemView = Backbone.View.extend({
    tagName: 'li',
    className: 'list-menu-item',

    template: _.template(template),

    events: {
      'click': 'open'
    },

    initialize: function() {
      this.model.on('change', this.render, this);
      this.model.on('destroy', this.remove, this);
    },

    render: function() {
      var $el = $(this.el);
      $el.data('listId', this.model.get('id'));
      $el.html(this.template(this.model.toJSON()));
      return this;
    },

    open: function() {
      var self = this;
      return false;
    }
  });

  return ListMenuItemView;
});
{% endhighlight %}

The template is `app/js/templates/lists/menuitem.html`:

{% highlight html %}
<a href="#" class="list-title" data-list-id="{{id}}">{{title}}</a>
{% endhighlight %}

Notice that curly braces are used to insert values.  This is provided by Underscore's built-in template system.

The view's `open` method is bound to `click` events, and I've also bound `change` and `destroy` model events to the view as well -- these will come in handy later.

The template's values are inserted by using the `template` method in `render`:

{% highlight javascript %}
$el.html(this.template(this.model.toJSON()));
{% endhighlight %}

The model's raw JSON is passed to `template` so `title` and `id` will be resolved to the correct values.

###Invoking `ListMenuView`

Open `app/js/app.js` and add `ListMenuView` to the list of `define` requirements:

{% highlight javascript %}
define([
  'gapi'
, 'views/app'
, 'views/auth'
, 'views/lists/menu'
, 'collections/tasklists'
],

function(ApiManager, AppView, AuthView, ListMenuView, TaskLists) {
{% endhighlight %}

Last week I added a `console.log` to print out the name of each list.  Remove that code and change it to render the `ListMenuView`:

{% highlight javascript %}
connectGapi: function() {
  var self = this;
  this.apiManager = new ApiManager(this);
  this.apiManager.on('ready', function() {
    self.collections.lists.fetch({ data: { userId: '@me' }, success: function(res) {
      self.views.listMenu.render();
    }});
  });
}
{% endhighlight %}

Go back up to the `App` constructor function to make it instantiate `listMenu` by passing the relevant collection:

{% highlight javascript %}
var App = function() {
  this.views.app = new AppView();
  this.views.app.render();
  this.views.auth = new AuthView(this);
  this.views.auth.render();
  this.collections.lists = new TaskLists();
  this.views.listMenu = new ListMenuView({ collection: this.collections.lists });

  this.connectGapi();
};
{% endhighlight %}

###Running It

Now if you run `node server` and visit `http://localhost:8080/`, you should see your task lists displayed in a simple unordered list.

###Summary

The app is now communicating with Google, allowing users to sign in, and also displays the user's task lists.  It still doesn't look too exciting because we haven't yet applied any styles, but you should be able to adapt the code you've seen so far to work with other Google APIs and similar services.

This tutorial's code is available in [commit 82fe08e on GitHub](https://github.com/alexyoung/dailyjs-backbone-tutorial/tree/82fe08ebff2cbc71350870dcd1a2c1b49f57f22d).

