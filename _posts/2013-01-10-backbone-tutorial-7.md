---
layout: post
title: "Backbone.js Tutorial: Editing Lists"
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
  <li><a href="http://dailyjs.com/2013/01/10/backbone-tutorial-7/"><strong>Part 7: Editing Lists</strong></a></li>
  <li><a href="http://dailyjs.com/2013/01/17/backbone-tutorial-8/">Part 8: Deleting Lists</a></li>
  <li><a href="http://dailyjs.com/2013/01/24/backbone-tutorial-9/">Part 9: Tasks</a></li>
  <li><a href="http://dailyjs.com/2013/01/31/backbone-tutorial-10/">Part 10: Oh No Not More Tasks</a></li>
  <li><a href="http://dailyjs.com/2013/02/07/backbone-tutorial-11/">Part 11: Spies, Stubs, and Mocks</a></li>
  <li><a href="http://dailyjs.com/2013/02/14/backbone-tutorial-12/">Part 12: Testing with Mocks</a></li>
  <li><a href="http://dailyjs.com/2013/03/07/backbone-tutorial-13/">Part 13: Routes</a></li>
</ul>

###Preparation

Before starting this tutorial, you'll need the following:

* [alexyoung / dailyjs-backbone-tutorial](https://github.com/alexyoung/dailyjs-backbone-tutorial) at commit `465523f`
* The API key from part 2
* The "Client ID" key from part 2
* Update `app/js/config.js` with your keys (if you've checked out my source)

To check out the source, run the following commands (or use a suitable Git GUI tool):

{% highlight text %}
git clone git@github.com:alexyoung/dailyjs-backbone-tutorial.git
cd dailyjs-backbone-tutorial
git reset --hard 465523f
{% endhighlight %}

###Active List

Last week I demonstrated how to make a custom `Backbone.sync` "create" implementation, and suitable views and templates for adding new lists.  If you recall, I created a view for editing lists as well, because it was so similar to `AddListView` it made sense to inherit from it.

Before a list can be edited, we need a way of selecting lists.  It makes sense to always have an active list in this application, so there should be a way of saving this state somewhere.  Also, when loading the lists from the server, a default list should be selected on the user's behalf.

To be consistent with the patterns employed to track collections and views, we should add a `models` object for tracking instances of models.  One of these can be the `activeList`.

Open `app/js/app.js` and add a `models` property as well as setting the `activeModel` after the lists have loaded:

{% highlight javascript %}
App.prototype = {
  views: {},
  collections: {},
  models: {},
  connectGapi: function() {
    var self = this;
    this.apiManager = new ApiManager(this);
    this.apiManager.on('ready', function() {
      self.collections.lists.fetch({ data: { userId: '@me' }, success: function(res) {
        self.models.activeList = self.collections.lists.first();
        self.views.listMenu.render();
      }});
    });
  }
};
{% endhighlight %}

Now open `app/js/views/lists/menu.js` and make it check if the `activeModel` is the model currently being used to render the navigation list element:

{% highlight javascript %}
renderMenuItem: function(model) {
  var item = new ListMenuItemView({ model: model });
  this.$el.append(item.render().el);

  if (model.get('id') === bTask.models.activeList.get('id')) {
    item.open();
  }
},
{% endhighlight %}

If the model does match, then it'll trigger an `open` on the view.  Now open `app/js/views/lists/menuitem.js` and make the `ListMenuItemView` track the `activeModel`:

{% highlight javascript %}
open: function() {
  bTask.models.activeList = this.model;
  return false;
}
{% endhighlight %}

Now the application is able to track the selected list.  This will make adding tasks easier, because in order to add tasks we need to know which tasklist to add it to.

###Edit List Form

Open `app/js/views/app.js`.  The goal of this exercise is to make the edit form appear, filled out with the correct values, when the "Edit List" link is clicked.  It's going to be similar to last week's `addList` method, so you can try doing this part yourself if you want.

First, make it load the `EditListView` class:

{% highlight javascript %}
define([
  'text!templates/app.html'
, 'views/lists/add'
, 'views/lists/edit'
],

function(template, AddListView, EditListView) {
{% endhighlight %}

Next, add the `#edit-list-button` to the events:

{% highlight javascript %}
events: {
  'click #add-list-button': 'addList'
, 'click #edit-list-button': 'editList'
},
{% endhighlight %}

Finally, add the `editList` method to instantiate an `EditListView` form based on the `activeList`:

{% highlight javascript %}
editList: function() {
  var form = new EditListView({ model: bTask.models.activeList });

  this.$el.find('#list-editor').html(form.render().el);
  form.$el.find('input:first').focus();

  return false;
}
{% endhighlight %}

This is very similar to the `addList` method -- they could easily use the same method, just with different models:

{% highlight javascript %}
listForm: function(form) {
  this.$el.find('#list-editor').html(form.render().el);
  form.$el.find('input:first').focus();

  return false;
},

addList: function() {
  return this.listForm(new AddListView({ model: new bTask.collections.lists.model({ title: '' }) }));
},

editList: function() {
  return this.listForm(new EditListView({ model: bTask.models.activeList }));
}
{% endhighlight %}

DRY!

###Saving Changes

The `Backbone.sync` method needs to be updated to cope with updating items.  This is _very_ similar to creating items (in `app/js/gapi.js`):

{% highlight javascript %}
// Around line 97, after 'create'
case 'update':
  requestContent['resource'] = model.toJSON();
  request = gapi.client.tasks[model.url].update(requestContent);
  Backbone.gapiRequest(request, method, model, options);
break;
{% endhighlight %}

A slight complication is Google's API requires a `tasklist` property in the object passed to `update`.  This isn't very clearly documented (you'll notice the [tasklists/update](https://developers.google.com/google-apps/tasks/v1/reference/tasklists/update) reference doesn't have a JavaScript example).

Rather than making the Backbone models somehow aware of this, it's better to put the logic in `Backbone.sync`.  That way all of the Google-related stuff is in the same place.

Add another `switch` statement to insert the required ID parameters, based on the type of model being operated on:

{% highlight javascript %}
Backbone.sync = function(method, model, options) {
  var requestContent = {};
  options || (options = {});

  switch (model.url) {
    case 'tasks':
      requestContent.task = model.get('id');
    break;

    case 'tasklists':
      requestContent.tasklist = model.get('id');
    break;
  }
{% endhighlight %}

The lists should now be editable, but there's one thing left to do -- show that the selected list is "active".

###Selecting Lists

Open `app/js/views/lists/menuitem.js` and change `open` to track the active menu view, and add a class name to the view's element:

{% highlight javascript %}
open: function() {
  if (bTask.views.activeListMenuItem) {
    bTask.views.activeListMenuItem.$el.removeClass('active');
  }

  bTask.models.activeList = this.model;
  bTask.views.activeListMenuItem = this;
  this.$el.addClass('active');

  return false;
}
{% endhighlight %}

Whenever a view is opened, `bTask.views.activeListMenuItem` will be used to store a reference to it.  Notice how I've used `this.$el`?  Most experienced Backbone developers will tell you to do this, rather than using jQuery's `$()` to find elements based on a selector.  The idea is to use minimal jQuery and be more declarative with Backbone.

Does keeping a reference to `bTask.views.activeListMenuItem` beat `$('.list-menu-item').removeClass('active')`?  It's hard to say -- I've often noticed people dipping into jQuery where it makes sense.

This begs the question: should we really track the active list using a reference to a model?  The `ListMenuItemView` already contains a reference to the model, and most of the Backbone code is really concerned with modeling the user interface, rather than an additional internal state.  Let's try removing the reference to `bTask.models`.

Open `app/js/app.js` and remove the `models` object, and then remove the line that sets `activeList`.  Next, go to `app/js/views/lists/menuitem.js` and change the `open` method to only refer to views:

{% highlight javascript %}
open: function() {
  if (bTask.views.activeListMenuItem) {
    bTask.views.activeListMenuItem.$el.removeClass('active');
  }

  bTask.views.activeListMenuItem = this;
  this.$el.addClass('active');

  return false;
}
{% endhighlight %}

Next open the `AppView` class, in `app/js/views/app.js`, and make sure `editList` uses `bTask.views.activeListMenuItem.model`.  Finally, make `app/js/views/lists/menu.js` activate the default item (the first list):

{% highlight javascript %}
renderMenuItem: function(model) {
  var item = new ListMenuItemView({ model: model });
  this.$el.append(item.render().el);

  if (!bTask.views.activeListMenuItem) {
    bTask.views.activeListMenuItem = item;
  }
  
  if (model.get('id') === bTask.views.activeListMenuItem.model.get('id')) {
    item.open();
  }
},
{% endhighlight %}

I feel like avoiding tracking an internal application state is a mistake in Backbone, and instead the views should be made to work harder.  Is this a good idea?  It probably depends on the nature of the application.

To make the interface clearer, you can add `li.active { font-weight: bold }` to `app/css/app.css`.

###Summary

In this part we've built on the code in _Part 6_ to allow lists to be edited.  Even though this is fairly simple, the application had to change to track the currently active list.

The general rule of thumb in Backbone is to use cached jQuery (or Zepto) objects, which is why you'll see a lot of calls to `this.$el` rather than `$()`.  I suggest another rule that complements this: make views do the work, and avoid relying on state external to views.

The full source for this tutorial can be found in [alexyoung / dailyjs-backbone-tutorial, commit 0953c5d](https://github.com/alexyoung/dailyjs-backbone-tutorial/tree/0953c5d7873fe3f7d176984e0337724be2b3386f).

