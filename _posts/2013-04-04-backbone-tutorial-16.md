---
layout: post
title: "Backbone.js Tutorial: jQuery Plugins and Moving Tasks"
author: Alex Young
categories: 
- backbone.js
- mvc
- node
- backgoog
- bootstrap
- jquery
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
  <li><a href="http://dailyjs.com/2013/03/07/backbone-tutorial-13/">Part 13: Routes</a></li>
  <li><a href="http://dailyjs.com/2013/03/14/backbone-tutorial-14/">Part 14: Customising the UI</a></li>
  <li><a href="http://dailyjs.com/2013/03/28/backbone-tutorial-15/">Part 15: Updates for 1.0, Clear Complete</a></li>
  <li><a href="http://dailyjs.com/2013/04/04/backbone-tutorial-16/"><strong>Part 16: jQuery Plugins</strong></a></li>
</ul>

###Preparation

Before starting this tutorial, you'll need the following:

* [alexyoung / dailyjs-backbone-tutorial](https://github.com/alexyoung/dailyjs-backbone-tutorial) at commit `705bcb4`
* The API key from part 2
* The "Client ID" key from part 2
* Update `app/js/config.js` with your keys (if you've checked out my source)

To check out the source, run the following commands (or use a suitable Git GUI tool):

{% highlight text %}
git clone git@github.com:alexyoung/dailyjs-backbone-tutorial.git
cd dailyjs-backbone-tutorial
git reset --hard 705bcb4
{% endhighlight %}

###Using Backbone with jQuery Plugins

Although Backbone doesn't need to be used with jQuery specifically, a lot of people use it with jQuery (and RequireJS) to get access to the diverse plugins made by the jQuery community.  In this tutorial I'll explain how to use jQuery plugins with Backbone projects, and how to find ones that will work well.

The example I've used is integrating a drag-and-drop "sortable" plugin to allow tasks to be reordered.

###HTML5 Sortable

The plugin I've used for drag-and-drop is the [HTML5 Sortable Plugin](http://farhadi.ir/projects/html5sortable) by Ali Farhadi.  The reason I used this particular plugin is it has a simple event-based API that allows the plugin to be unloaded and sort events to be captured and responded to.  It just needs a container element and the child elements that need to be sorted.  The unordered list of tasks in this project directly translates to the expected markup.

Sometimes it's easier to just write out data attributes to elements rather than trying to create relationships between the DOM nodes used by plugins and models.  HTML5 Sortable emits a `'sortupdate'` event when a node has been dragged and dropped, and it'll pass the relevant element to the listener callback.  From this we need to figure out which model has changed, then translate that into something Google's API can understand.

###Loading Plugins with RequireJS

In an earlier tutorial I demonstrated how to load non-AMD libraries using RequireJS.  If you want a recap, just check out `app/js/main.js` and look at the `shim` property in the RequireJS configuration:

{% highlight javascript %}
requirejs.config({
  baseUrl: 'js',

  paths: {
    text: 'lib/text'
  },

  shim: {
    'lib/underscore-min': {
      exports: '_'
    },
    'lib/backbone': {
      deps: ['lib/underscore-min']
    , exports: 'Backbone'
    },
    'app': {
      deps: ['lib/underscore-min', 'lib/backbone', 'lib/jquery.sortable']
    }
  }
});
{% endhighlight %}

The `'app'` property expresses a dependency between the main Backbone application file and `lib/jquery.sortable`, which means `/lib/jquery.sortable.js` will get automatically loaded (or compiled in by `r.js` when creating a production build of the app).

###Google Tasks Ordering API

It would be too easy if HTML5 Sortable's API was a one-to-one match with the Google Task's ordering API.  Google's API has a specific method for moving tasks, and it's based around moving one task to occupy the position of another one:

{% highlight javascript %}
gapi.client.tasks.tasks.move({ tasklist: listId, task: id, previous: previousId });
{% endhighlight %}

Moving a task to the top of the list is handled by passing `null` for `previous`.

Next I'll explain how to create some simple interface elements for the draggable handle, and then we'll look at how to persist moved tasks by translating Google's API into Backbone model and collection code.

###Implementation: Views and Templates

I added a little handle by using a Bootstrap icon and an anchor element in `app/js/templates/tasks/task.html`:

{% highlight html %}
<a href="#" class="handle pull-right"><i class="icon-move"></i></a>
{% endhighlight %}

Next I added the code that maps between the Backbone view and the jQuery HTML5 Sortable plugin to `app/js/views/tasks/index.js`:

{% highlight javascript %}
makeSortable: function() {
  var $el = this.$el.find('#task-list');
  if (this.collection.length) {
    $el.sortable('destroy');
    $el.sortable({ handle: '.handle' }).bind('sortupdate', _.bind(this.saveTaskOrder, this));
  }
},

saveTaskOrder: function(e, o) {
  var id = $(o.item).find('.check-task').data('taskId')
    , previous = $(o.item).prev()
    , previousId = previous.length ? $(previous).find('.check-task').data('taskId') : null
    , request
    ;

  this.collection.move(id, previousId, this.model);
},
{% endhighlight %}

The `makeSortable` method makes an element that appears within `TasksIndexView` "sortable" -- that is, HTML Sortable has been wrapped around it.  The plugin's `'sortupdate'` method is then bound to `saveTaskOrder`.

The `saveTaskOrder` method gets the current task's ID by looking at the checkbox, because I'd already added a data attribute to that element in the template.  This ID is then passed to the collection with the previous task's ID.  In this case, the previous task is the one adjacent to it, which Google's API needs to figure out how to move the task.

The collection property in this view is a `Tasks` property, so let's take a look at how to implement the `move` method that causes the changes to be persisted.

###Implementation: Models and Collections

Open `app/js/collections/tasks.js` and add a new method called `move`:

{% highlight javascript %}
move: function(id, previousId, list) {
  var model = this.get(id)
    , toModel = this.get(previousId)
    , index = this.indexOf(toModel) + 1
    ;

  this.remove(model, { silent: true });
  this.add(model, { at: index, silent: true });

  // Persist the change
  list.moveTask({ task: id, previous: previousId });
}
{% endhighlight %}

This method just exists to trigger `remove` and `add` calls on the collection so cause the objects to be reshuffled internally.  It then calls `moveTask` on the `TaskList` model (in `app/js/models/tasklist.js`):

{% highlight javascript %}
moveTask: function(options) {
  options['tasklist'] = this.get('id');
  var request = gapi.client.tasks.tasks.move(options);

  Backbone.gapiRequest(request, 'update', this, options);
}
{% endhighlight %}

The `gapiRequest` method forms the basis for the custom `Backbone.sync` method used in this project, which I've talked about in previous tutorials.  I wasn't able to figure out how to make `Backbone.sync` cope with moving items in a way that made sense given how `gapi.client.tasks.tasks.move` works, but I was able to at least reuse some of the syncing functionality by creating a request and calling the "standard" request handler.

###Summary

When you can't find a suitable Backbone plugin for something and want to use a jQuery plugin, my advice is to look for plugins that have event-based APIs and can be cleanly unloaded.  That will make them easy to hook into your Backbone views.

The full source for this tutorial can be found in [alexyoung / dailyjs-backbone-tutorial, commit e9edfa3](https://github.com/alexyoung/dailyjs-backbone-tutorial/commit/e9edfa3157fd460a9c82faa6c6bb9d87ccdca443).
