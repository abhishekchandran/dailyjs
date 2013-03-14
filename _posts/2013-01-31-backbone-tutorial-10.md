---
layout: post
title: "Backbone.js Tutorial: Oh No, Not More Tasks"
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
  <li><a href="http://dailyjs.com/2013/01/31/backbone-tutorial-10/"><strong>Part 10: Oh No Not More Tasks</strong></a></li>
  <li><a href="http://dailyjs.com/2013/02/07/backbone-tutorial-11/">Part 11: Spies, Stubs, and Mocks</a></li>
  <li><a href="http://dailyjs.com/2013/02/14/backbone-tutorial-12/">Part 12: Testing with Mocks</a></li>
  <li><a href="http://dailyjs.com/2013/03/07/backbone-tutorial-13/">Part 13: Routes</a></li>
  <li><a href="http://dailyjs.com/2013/03/14/backbone-tutorial-14/">Part 14: Customosing the UI</a></li>
</ul>

###Preparation

Before starting this tutorial, you'll need the following:

* [alexyoung / dailyjs-backbone-tutorial](https://github.com/alexyoung/dailyjs-backbone-tutorial) at commit `0491ad`
* The API key from part 2
* The "Client ID" key from part 2
* Update `app/js/config.js` with your keys (if you've checked out my source)

To check out the source, run the following commands (or use a suitable Git GUI tool):

{% highlight text %}
git clone git@github.com:alexyoung/dailyjs-backbone-tutorial.git
cd dailyjs-backbone-tutorial
git reset --hard 0491ad
{% endhighlight %}

###Tasks Continued

<div class="image">
  <img src="/images/posts/backbone-part-10.png" alt="" />
  <small>A preview of today's tutorial.</small>
</div>

The application is now displaying lists of tasks, but you can't yet interact with them.  This tutorial will cover:

* Adding tasks
* Editing tasks
* Deleting tasks
* Toggling tasks

Most of this content builds on what we did with lists, but it'll be good practice if you're looking for more experience with Backbone.

###Adding Tasks

Open `app/js/views/tasks/index.js` and ensure there's an event binding for `addTask`:

{% highlight javascript %}
events: {
  'submit .add-task': 'addTask'
},
{% endhighlight %}

In the `initialize` method, add a listener to this class's collection:

{% highlight javascript %}
initialize: function() {
  this.children = [];
  this.collection.on('add', this.renderTask, this);
},
{% endhighlight %}

This will make it automatically render new tasks when they're added to the collection.

The `addTask` method should call `Task.prototype.save` to persist the task using Google's API, after instantiating it with a reference to the current list.  It should also render the task once it's been saved.  I've passed in `{ at: 0}` because Google Tasks places new tasks at the top of a list.  Notice that I prefer to only add tasks once they've been successfully saved -- that makes this application always require an Internet connection.  It may be preferable to save to a local database and sync with Google later, but we're not going to do that here.

{% highlight javascript %}
addTask: function() {
  var $input = this.$el.find('input[name="title"]')
    , task = new this.collection.model({ tasklist: this.model.get('id') })
    , self = this
    ;

  task.save({ title: $input.val() }, {
    success: function() {
      self.collection.add(task, { at: 0 });
    }
  });
  $input.val('');

  return false;
},

renderTask: function(task, list, options) {
  var item = new TaskView({ model: task, parentView: this })
    , $el = this.$el.find('#task-list');
  if (options && options.at === 0) {
    $el.prepend(item.render().el);
  } else {
    $el.append(item.render().el);
  }
  this.children.push(item);
},
{% endhighlight %}

The `renderTask` method will receive the `options` argument, and it uses it to determine how to add the task to the list.  The reason I don't just prepend new tasks is the `render` method can now be refactored to use this method:

{% highlight javascript %}
render: function() {
  this.$el.html(this.template());

  var $el = this.$el.find('#task-list')
    , self = this;

  this.collection.fetch({ data: { tasklist: this.model.get('id') }, success: function() {
    self.collection.each(function(task) {
      task.set('tasklist', self.model.get('id'));
      self.renderTask(task);
    });
  }});
}
{% endhighlight %}

Open `app/js/views/lists/menuitem.js` and make it pass in a `Tasks` collection in the `open` method where it instantiates `bTask.views.tasksIndexView`:

{% highlight javascript %}
bTask.views.tasksIndexView = new TasksIndexView({ collection: new Tasks({ tasklist: this.model.get('id') }), model: this.model });
{% endhighlight %}

You'll need to change the `define` statement at the top of the file to include the `Tasks` collection:

{% highlight javascript %}
define(['text!templates/lists/menuitem.html', 'views/tasks/index', 'collections/tasks'], function(template, TasksIndexView, Tasks) {
{% endhighlight %}

Due to how Google's API works, you'll need to make a small change to `app/js/gapi.js` to insert a `tasklist` ID into the `requestContent` payload:

{% highlight javascript %}
Backbone.sync = function(method, model, options) {
  var requestContent = {};
  options || (options = {});

  switch (model.url) {
    case 'tasks':
      requestContent.task = model.get('id');
      requestContent.tasklist = model.get('tasklist');
    break;
{% endhighlight %}

Adding tasks should now work -- there's no need for a new template because it's already been added as part of last week's tutorial.

###Editing Tasks

To edit tasks, a few things are needed:

* A suitable form template
* A `Backbone.View`
* Event handling for saving the task

Here's the template, which should be saved to `app/js/templates/tasks/edit.html`:

{% highlight html %}
<fieldset>
  <legend>
    Task Properties
    <a href="#" data-task-id="{{id}}" class="pull-right delete-task btn"><i class="icon-trash"></i></a>
  </legend>
  <div class="control-group">
    <label for="task_title">Title</label>
    <input type="text" class="input-block-level" name="title" id="task_title" value="{{title}}" placeholder="The task's title">
  </div>
  <div class="control-group">
    <label class="radio"><input type="radio" name="status" value="needsAction" {{status === 'needsAction' ? 'checked' : '' }}> Needs action</label>
    <label class="radio"><input type="radio" name="status" value="completed" {{status === 'completed' ? 'checked' : '' }}> Complete</label>
  </div>
  </div>
  <div class="control-group">
    <label for="task_notes">Notes</label>
    <textarea class="input-block-level" name="notes" id="task_notes" placeholder="Notes about this task">{{notes}}</textarea>
  </div>
</fieldset>
<div class="form-actions">
  <button type="submit" class="btn btn-primary">Save Changes</button>
  <button class="cancel btn">Close</button>
</div>
{% endhighlight %}

I've included all of the usual Bootstrap classes and markup in this form fragment so it will look nice when it's rendered.

The corresponding view (`app/js/views/tasks/edit.js`) should look like this:

{% highlight javascript %}
define(['text!templates/tasks/edit.html'], function(template) {
  var TaskEditView = Backbone.View.extend({
    tagName: 'form',
    className: 'well edit-task',
    template: _.template(template),

    events: {
      'submit': 'submit'
    , 'click .cancel': 'cancel'
    },

    initialize: function() {
      this.model.on('change', this.render, this);
    },

    render: function() {
      this.$el.html(this.template(this.model.toJSON()));
      return this;
    },

    submit: function() {
      var title = this.$el.find('input[name="title"]').val()
        , notes = this.$el.find('textarea[name="notes"]').val()
        , status = this.$el.find('input[name="status"]:checked').val()
        ;

      this.model.set('title', title);
      this.model.set('notes', notes);

      if (status !== this.model.get('status')) {
        this.model.set('status', status);
        if (status === 'needsAction') {
          this.model.set('completed', null);
        }
      }

      this.model.save();
      return false;
    },

    cancel: function() {
      this.remove();
      return false;
    }
  });

  return TaskEditView;
});
{% endhighlight %}

This sets up a `submit` event for catching the form submission, and also an event for closing the form, which is what the `cancel` method is for.

Now add a method to `app/js/views/tasks/index.js` that invokes `TaskEditView`:

{% highlight javascript %}
editTask: function(task) {
  if (this.taskEditView) {
    this.taskEditView.remove();
  }
  this.taskEditView = new TaskEditView({ model: task });
  this.$el.find('#selected-task').append(this.taskEditView.render().el);
}
{% endhighlight %}

And make sure it loads `TaskEditView`:

{% highlight javascript %}
define(['text!templates/tasks/index.html', 'views/tasks/task', 'views/tasks/edit', 'collections/tasks'], function(template, TaskView, TaskEditView, Tasks) {
{% endhighlight %}

This needs to be called by an individual task, so open `app/js/views/tasks/task.js` and add this to the `open` method:

{% highlight javascript %}
this.parentView.editTask(this.model);
{% endhighlight %}

These two views have a lot of coupling between them, which makes `TaskView` difficult to reuse.  However, is it likely that it'll make sense to use it without `TasksIndexView`?  That's the kind of question you'll ask yourself a lot when trying to write maintainable Backbone code.

###Deleting Tasks

Add a `destroy` method to `app/js/views/tasks/edit.js`:

{% highlight javascript %}
destroy: function() {
  this.model.destroy();
  return false;
}
{% endhighlight %}

Then bind the method to the event on the trash can icon (`.delete-task`) and also bind an event to the model being deleted:

{% highlight javascript %}
events: {
  'submit': 'submit'
, 'click .cancel': 'cancel'
, 'click .delete-task': 'destroy'
},

initialize: function() {
  this.model.on('change', this.render, this);
  this.model.on('destroy', this.remove, this);
},
{% endhighlight %}

###Toggling Tasks

Here's the icing on the cake, toggling the task status!  With this change, the app will really start to feel like a real to-do list app.  Open `app/js/views/tasks/task.js` and add an event binding for the checkboxes in the list -- a `change` event is required for this:

{% highlight javascript %}
events: {
  'click': 'open'
, 'change .check-task': 'toggle'
},
{% endhighlight %}

Then the `toggle` method just needs to toggle the `status` attribute based on the checkbox's state:

{% highlight javascript %}
toggle: function() {
  var id = this.model.get('id')
    , $el = this.$el.find('.check-task')
    ;

  this.model.set('status', $el.attr('checked') ? 'completed' : 'needsAction');
  if (this.model.get('status') === 'needsAction') {
    this.model.set('completed', null);
  }

  this.model.save();
  return false;
}
{% endhighlight %}

Google's nomenclature for the task state is `completed` and `needsAction`, which takes a bit of digging in the documentation to find out.

###Summary

It's taken a while to get this far, but working with unfamiliar APIs with their idiosyncrasies can take a lot of patience.  And if you try running the code from this project, make sure you actually have some tasks and lists in Gmail already -- [it doesn't work tell well without any](https://github.com/alexyoung/dailyjs-backbone-tutorial/issues/3). I'll fix it later!

The full source for this tutorial can be found in [alexyoung / dailyjs-backbone-tutorial, commit 9691fc1](https://github.com/alexyoung/dailyjs-backbone-tutorial/commit/9691fc13dbcfd8adbd604c5974291011ce7148f8).

