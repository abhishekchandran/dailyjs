---
layout: post
title: "Backbone.js Tutorial: Creating Lists"
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
  <li><a href="http://dailyjs.com/2013/01/03/backbone-tutorial-6/"><strong>Part 6: Creating Lists</strong></a></li>
  <li><a href="http://dailyjs.com/2013/01/10/backbone-tutorial-7/">Part 7: Editing Lists</a></li>
  <li><a href="http://dailyjs.com/2013/01/17/backbone-tutorial-8/">Part 8: Deleting Lists</a></li>
  <li><a href="http://dailyjs.com/2013/01/24/backbone-tutorial-9/">Part 9: Tasks</a></li>
  <li><a href="http://dailyjs.com/2013/01/31/backbone-tutorial-10/">Part 10: Oh No Not More Tasks</a></li>
  <li><a href="http://dailyjs.com/2013/02/07/backbone-tutorial-11/">Part 11: Spies, Stubs, and Mocks</a></li>
  <li><a href="http://dailyjs.com/2013/02/14/backbone-tutorial-12/">Part 12: Testing with Mocks</a></li>
  <li><a href="http://dailyjs.com/2013/03/07/backbone-tutorial-13/">Part 13: Routes</a></li>
  <li><a href="http://dailyjs.com/2013/03/14/backbone-tutorial-14/">Part 14: Customosing the UI</a></li>
  <li><a href="http://dailyjs.com/2013/03/28/backbone-tutorial-15/">Part 15: Updates for 1.0, Clear Complete</a></li>
</ul>

###Preparation

Before starting this tutorial, you'll need the following:

* [alexyoung / dailyjs-backbone-tutorial](https://github.com/alexyoung/dailyjs-backbone-tutorial) at commit `82fe08e`
* The API key from part 2
* The "Client ID" key from part 2
* Update `app/js/config.js` with your keys (if you've checked out my source)

To check out the source, run the following commands (or use a suitable Git GUI tool):

{% highlight text %}
git clone git@github.com:alexyoung/dailyjs-backbone-tutorial.git
cd dailyjs-backbone-tutorial
git reset --hard 82fe08e
{% endhighlight %}

###List CRUD

The last few parts of this tutorial series have demonstrated how to talk to Google's Tasks API and authenticate with OAuth.  At this point, you should be able to sign in and see a list of task lists.

As we've seen, Backbone.js is based around RESTful APIs that speak in terms of CRUD (create, read, update and delete).  In [Part 4](http://dailyjs.com/2012/12/20/backbone-tutorial-4/), I explained how to write a custom `Backbone.sync` method that can communicate with Google's APIs, but so far we've only implemented "read" functionality, which fetches task lists using `gapi.client.tasks`.

Now we really need to implement the full set of CRUD operations so users can manage lists.  Part 4 showed how Google's API maps to Backbone's `sync` operations:

<table class="amy">
  <thead>
    <tr>
      <th>Google Tasks API</th><th>Backbone.sync Method</th><th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><code>insert</code></td><td><code>create</code></td><td>Create a new task.</td>
    </tr>
    <tr>
      <td><code>update</code></td><td><code>update</code></td><td>Update an existing task.</td>
    </tr>
    <tr>
      <td><code>delete</code></td><td><code>delete</code></td><td>Delete a task.</td>
    </tr>
    <tr>
      <td><code>list</code></td><td><code>read</code></td><td>Get a list of tasks.</td>
    </tr>
  </tbody>
</table>

In this part we'll add support for "create", but as you'll see the principles are very similar to the "read" implementation.

###Creating Lists

In order to create lists, several new components are required:

1. Suitable buttons
2. A form template
3. Add and edit views
4. Controller code

In Backbone.js, models and collections emit events.  We've already created code to manage list item views, so all we need to do is hook this up to the event that fires when a new model is created and added to the `TaskLists` collection.

Mastering and exploiting events in this way is one of the tricks to writing manageable Backbone.js code.

###Backbone.sync

So far, `Backbone.sync` can only read lists from Google's API.  To make it capable of creating items we'll need a little bit of extra code.  This will build upon what we've already written, so it'll be short and sweet.

Go back to `app/js/gapi.js` and change `Backbone.sync` to call `gapiRequest` when the `create` operation is invoked:

{% highlight javascript %}
Backbone.sync = function(method, model, options) {
  var requestContent = {};
  options || (options = {});

  switch (method) {
    case 'create':
      requestContent['resource'] = model.toJSON();
      request = gapi.client.tasks[model.url].insert(requestContent);
      Backbone.gapiRequest(request, method, model, options);
    break;
{% endhighlight %}

This looks a lot like the "read" code.  There is one more thing we need to do in this file -- change `Backbone.gapiRequest` to deal with single resources.  I've put the full code for the method below because it's still short with the modifications for this tutorial:

{% highlight javascript %}
Backbone.gapiRequest = function(request, method, model, options) {
  var result;
  request.execute(function(res) {
    if (res.error) {
      if (options.error) options.error(res);
    } else if (options.success) {
      if (res.items) {
        result = res.items;
      } else {
        result = res;
      }
      options.success(result, true, request);
    }
  });
};
{% endhighlight %}

This looks to see if an array of items has been returned by Google's API, or simply a single object.  There's an important lesson here though: `Backbone.sync` is sandwiched between other Backbone code, and is capable of providing Backbone with properties that will be used to set model attributes later on.  This code doesn't look like it does much, but the `success` callback will receive `result`, which will have an `id` property when models are created.  Backbone will see this `id` property and use it to set the model's `id` attribute, automatically!

Many Bothans died to bring us this information.

###Template Junk

Open `app/js/templates/app.html` and update the `signed-in-container` `div` to contain a list and another container `div`:

{% highlight html %}
<ul class="nav nav-tabs" id="top-nav">
  <li class="buttons">
    <div class="btn-group">
      <a href="#" class="btn" id="add-list-button"><i class="icon-plus">Add List</i></a>
      <a href="#" class="btn" id="edit-list-button"><i class="icon-cog">Edit List</i></a>
      <a href="#" class="btn delete-list" id="delete-list-button"><i class="icon-trash">Delete List</i></a>
    </div>
  </li>
</ul>
<div id="content-container">
  <div id="list-editor"></div>
  <div id="tasks-container"></div>
</div>
{% endhighlight %}

This has the "Add List" button that you'll be able to use by the end of this tutorial, and it also has a `div` that'll contain the list add/edit form.

Now open `app/js/templates/lists/form.html` and paste this in:

{% highlight html %}
<fieldset>
  <legend>
    <span class="form-title">Edit List</span>
    <a href="#" class="pull-right delete-list btn"><i class="icon-trash"></i></a>
  </legend>
  <div class="control-group">
    <label class="control-label" for="list_title">Title</label>
    <div class="controls">
      <input type="text" class="input-xlarge" name="title" id="list_title" value="{{title}}" placeholder="The list's title">
    </div>
  </div>
</fieldset>
<div class="form-actions">
  <button type="submit" class="btn btn-primary">Save Changes</button>
  <button class="cancel btn">Close</button>
</div>
{% endhighlight %}

This is the body of a form that will be used to add or edit lists.  It uses the variable interpolation features we've already seen in this tutorial series.

###Add and Edit Views

I'm only going to cover adding lists in this tutorial, we'll get to the other functionality later (mainly because I've been writing this for three hours and I have client work to do and I need to pay the bills).  Bill-paying aside, what's the difference between an "add" and "edit" view?  The `form.html` template can be reused by both, so why don't we create an edit view and just inherit from it to make the list add view?

Open `app/js/views/lists/edit.js` and add this new view:

{% highlight javascript %}
define(['text!templates/lists/form.html'], function(template) {
  var EditListView = Backbone.View.extend({
    tagName: 'form',
    className: 'form-horizontal well edit-list',
    template: _.template(template),

    events: {
      'submit': 'submit'
    , 'click .cancel': 'cancel'
    },

    initialize: function() {
      this.model.on('change', this.render, this);
    },

    render: function() {
      var $el = $(this.el);
      $el.html(this.template(this.model.toJSON()));

      if (!this.model.get('id')) {
        this.$el.find('legend').html('Add List');
      }

      return this;
    },

    submit: function() {
      var self = this
        , title = this.$el.find('input[name="title"]').val()
        ;

      this.model.save({ title: title }, {
        success: function() {
          self.remove();
        }
      });

      return false;
    },

    cancel: function() {
      this.$el.hide();
      return false;
    }
  });

  return EditListView;
});
{% endhighlight %}

In this class, I've declared events for submitting and closing the form, and bound them to suitable methods.  I've also bound the `change` event on the view's model to `render`, so changes to the model will automatically get displayed.  This will be important later on.

Notice that in `render`, the `legend` will be changed when the model doesn't yet have an id.  In other words, when the model is new and hasn't been saved, show a different title and hide the delete button.

Now compare this file to `app/js/views/lists/add.js`:

{% highlight javascript %}
define([
'models/tasklist'
, 'views/lists/edit'
],

function(TaskList, EditListView) {
var AddListView = EditListView.extend({
  submit: function() {
    var self = this
      , title = this.$el.find('input[name="title"]').val()
      ;

    this.model.save({ title: title }, { success: function(model) {
      // Add the updated model to the collection
      bTask.collections.lists.add(model);
      self.remove();
    }});

    return false;
  }
});

return AddListView;
});
{% endhighlight %}

This file uses RequireJS to load `EditListView`, and then inherits from it.  The `submit` method is replaced because creating lists is slightly different to updating them.  When lists are created, it'll receive an updated model from the server in the `success` callback, which can be added to the global `lists` collection.  The view removes itself afterwards.

###Add List Button

A link for adding lists was added to the main `app.html` template earlier on.  To hook it up, open `app/js/views/app.js` and add a new method called `addList`:

{% highlight javascript %}
addList: function() {
  var list = new bTask.collections.lists.model({ title: '' })
    , form = new AddListView({ model: list })
    , self = this
    ;

  this.$el.find('#list-editor').html(form.render().el);
  form.$el.find('input:first').focus();

  return false;
}
{% endhighlight %}

This will render the `AddListView` template and focus on the title field.  You'll also have to change the top of the file to load `AddListView`:

{% highlight javascript %}
define([
  'text!templates/app.html'
, 'views/lists/add'
],

function(template, AddListView) {
{% endhighlight %}

Finally, add the events bindings somewhere in `AppView`:

{% highlight javascript %}
events: {
  'click #add-list-button': 'addList'
},
{% endhighlight %}

###Summary

![Adding Lists](/images/posts/backbone-tutorial-6.png)

If you run `node server` and visit `http://localhost:8080`, you should now be able to add lists.  The project doesn't _look_ particularly cool yet, but I'll get to that soon.

The full source for this tutorial can be found in [alexyoung / dailyjs-backbone-tutorial, commit 465523f](https://github.com/alexyoung/dailyjs-backbone-tutorial/tree/465523fa20c9f17a422de3646a8db5f7d1b707e8).

