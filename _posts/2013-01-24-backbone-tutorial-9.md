---
layout: post
title: "Backbone.js Tutorial: Tasks"
author: Alex Young
categories: 
- backbone.js
- mvc
- node
- backgoog
- fastfood
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
  <li><a href="http://dailyjs.com/2013/01/24/backbone-tutorial-9/"><strong>Part 9: Tasks</strong></a></li>
  <li><a href="http://dailyjs.com/2013/01/31/backbone-tutorial-10/">Part 10: Oh No Not More Tasks</a></li>
  <li><a href="http://dailyjs.com/2013/02/07/backbone-tutorial-11/">Part 11: Spies, Stubs, and Mocks</a></li>
  <li><a href="http://dailyjs.com/2013/02/14/backbone-tutorial-12/">Part 12: Testing with Mocks</a></li>
  <li><a href="http://dailyjs.com/2013/03/07/backbone-tutorial-13/">Part 13: Routes</a></li>
  <li><a href="http://dailyjs.com/2013/03/14/backbone-tutorial-14/">Part 14: Customosing the UI</a></li>
</ul>

###Preparation

Before starting this tutorial, you'll need the following:

* [alexyoung / dailyjs-backbone-tutorial](https://github.com/alexyoung/dailyjs-backbone-tutorial) at commit `8d88095`
* The API key from part 2
* The "Client ID" key from part 2
* Update `app/js/config.js` with your keys (if you've checked out my source)

To check out the source, run the following commands (or use a suitable Git GUI tool):

{% highlight text %}
git clone git@github.com:alexyoung/dailyjs-backbone-tutorial.git
cd dailyjs-backbone-tutorial
git reset --hard 8d88095
{% endhighlight %}

###Tasks CRUD

Things have been quiet in the Tasks Bootstrap project over the last few weeks.  Lists have appeared, but there's been nary a Hamburglar or Burger King in sight.  How do we attract those all important fast food mascots to our project?  By adding support for tasks of course!  How else can they write their extensive lists of upcoming franchise inspections and special edition McRibs?

This tutorial will cover the following:

* Creating a view for a single task
* Creating a view for a list of tasks
* Adding the tasks collection
* Fetching tasks from Google's API

The really interesting part that you'll want to remember is dealing with the relationship between a parent view and child views.  Backbone doesn't specifically address relationships between models, or views.  In this example, we ideally want to say _tasks belong to lists_ or _task views belong to list views_.  However, there isn't a de facto way of expressing such relationships.  There are libraries out there to do it, but I'll show you how to think about things in pure Backbone/Underscore.

###Boilerplate

Before you get started, create some new directories:

{% highlight text %}
$ mkdir app/js/views/tasks
$ mkdir app/js/templates/tasks
{% endhighlight %}

And add a new collection to `app/js/collections/tasks.js`:

{% highlight javascript %}
define(['models/task'], function(Task) {
  var Tasks = Backbone.Collection.extend({
    model: Task,
    url: 'tasks'
  });

  return Tasks;
});
{% endhighlight %}

The `Tasks` collection doesn't do anything you haven't seen before.  Fetching tasks with Google's API requires a `tasklist`, so you have to call `fetch` with an additional parameter:

{% highlight javascript %}
collection.fetch({ data: { tasklist: this.model.get('id') }, // ...
{% endhighlight %}

It's cool though, because we handled fetching `TaskLists` like that when we passed `{ userId: '@me' }` so it feels consistent within the context of this project.

The template that contains the tasks view includes a form for creating new tasks, a container for the task list, and another container for the currently selected task (so it can be edited).  This file should be saved as `app/js/templates/index.js`:

{% highlight html %}
<div class="span6">
  <div id="add-task">
    <form class="well row form-inline add-task">
      <input type="text" class="pull-left" placeholder="Enter a new task's title and press return" name="title">
      <button type="submit" class="pull-right btn"><i class="icon-plus"></i></button>
    </form>
  </div>
  <ul id="task-list"></ul>
</div>
<div class="span6">
  <div id="selected-task"></div>
  <div class="alert" id="warning-no-task-selected">
    <strong>Note:</strong> Select a task to edit or delete it.
  </div>
</div>
{% endhighlight %}

This uses some [Bootstrap](http://twitter.github.com/bootstrap/) classes for creating columns.  The `TaskView`, in `app/js/templates/tasks/task.html` has a few elements to contain the title, notes, and a checkbox for toggling the task's state:

{% highlight javascript %}
<input type="checkbox" data-task-id="{{id}}" name="task_check_{{id}}" class="check-task" value="t">
<span class="title {{status}}">{{title}}</span>
<span class="notes">{{notes}}</span>
{% endhighlight %}

###Views

The main `TasksIndexView` loads the tasks using the `Tasks` collection, and then renders them using `TaskView`.  This is the source for `TasksIndexView` in `app/js/views/tasks/index.js`:

{% highlight javascript %}
define(['text!templates/tasks/index.html', 'views/tasks/task', 'collections/tasks'], function(template, TaskView, Tasks) {
  var TasksIndexView = Backbone.View.extend({
    tagName: 'div',
    className: 'row-fluid',

    template: _.template(template),

    events: {
      'submit .add-task': 'addTask'
    },

    initialize: function() {
      this.children = [];
    },

    addTask: function() {
    },

    render: function() {
      this.$el.html(this.template());

      var $el = this.$el.find('#task-list')
        , self = this;

      this.collection = new Tasks();
      this.collection.fetch({ data: { tasklist: this.model.get('id') }, success: function() {
        self.collection.each(function(task) {
          var item = new TaskView({ model: task, parentView: self });
          $el.append(item.render().el);
          self.children.push(item);
        });
      }});

      return this;
    }
  });

  return TasksIndexView;
});
{% endhighlight %}

This loads the tasks using `collection.fetch`, and then appends a `TaskView` for each task.  This is `TaskView`:

{% highlight javascript %}
define(['text!templates/tasks/task.html'], function(template) {
  var TaskView = Backbone.View.extend({
    tagName: 'li',
    className: 'controls well task row',

    template: _.template(template),

    events: {
      'click': 'open'
    },

    initialize: function(options) {
      this.parentView = options.parentView;
    },

    render: function(e) {
      var $el = $(this.el);
      $el.data('taskId', this.model.get('id'));
      $el.html(this.template(this.model.toJSON()));
      $el.find('.check-task').attr('checked', this.model.get('status') === 'completed');

      return this;
    },

    open: function(e) {
      if (this.parentView.activeTaskView) {
        this.parentView.activeTaskView.close();
      }
      this.$el.addClass('active');
      this.parentView.activeTaskView = this;
    },

    close: function(e) {
      this.$el.removeClass('active');
    }
  });

  return TaskView;
});
{% endhighlight %}

The parent view is tracked so `open` can determine if another task has been clicked on, and if so "deactivate" it (remove the `active` class).  There are many ways to do this: I've seen people iterating over views to close all of them, using `$('selector').removeClass('active')` to remove all related items with an `active` class, or triggering events on models.  I feel like view-related code should be handled in views, and models and collections should do their own specific jobs.

Next you'll need to add `TasksIndexView` to the `define` in `app/js/views/lists/menuitem.js` and change the `open` method to instantiate a `TasksIndexView`:

{% highlight javascript %}
open: function() {
  if (bTask.views.activeListMenuItem) {
    bTask.views.activeListMenuItem.$el.removeClass('active');
  }

  bTask.views.activeListMenuItem = this;
  this.$el.addClass('active');

  // Render the tasks
  if (bTask.views.tasksIndexView) {
    bTask.views.tasksIndexView.remove();
  }

  bTask.views.tasksIndexView = new TasksIndexView({ collection: bTask.collections.tasks, model: this.model });
  bTask.views.app.$el.find('#tasks-container').html(bTask.views.tasksIndexView.render().el);

  return false;
}
{% endhighlight %}

It tracks the last instance of `TasksIndexView` so it can remove it manually.  It's usually a good idea to call `remove` so events can be unbound before views go out of scope -- I'll write a tutorial about Backbone and garbage collection later on.

I also added some defaults to the `Task` model (in `app/js/models/task.js`):

{% highlight javascript %}
define(function() {
  var Task = Backbone.Model.extend({
    url: 'tasks',
    defaults: { title: '', notes: '' }
  });

  return Task;
});
{% endhighlight %}

The reason I did this was the `TaskView` will raise errors when interpolating using a model that doesn't have a title or notes -- it's quite common for tasks in Google Tasks to not have any notes.

With these templates, views, and changes, you should be able to select lists and see their tasks, and also select tasks.

###Styles

![Bootstrap styles](/images/posts/backbone-9-styles.png)

As it stands, the application doesn't make a lot of visual sense.  I've added Bootstrap -- this just required downloading the CSS and image files and putting them in `app/css` and `app/img`.  Also, `app/index.html` loads `css/bootstrap.min.css`.

I added some custom styles to create a panel-based layout that shows the tasks in a similar way to [Things](http://culturedcode.com/things/).

###Backbone 0.9.10

I've updated Backbone to 0.9.10 and added it to the repository.  I had to change the `Backbone.sync` method to use a different signature when calling `options.success`, in `app/js/gapi.js`:

{% highlight javascript %}
options.success(model, result, request);
{% endhighlight %}

###Summary

The full source for this tutorial can be found in [alexyoung / dailyjs-backbone-tutorial, commit 0491ad](https://github.com/alexyoung/dailyjs-backbone-tutorial/commit/0491ad6e7de28ccfe0cab59138a93c469a3f2a7e).

