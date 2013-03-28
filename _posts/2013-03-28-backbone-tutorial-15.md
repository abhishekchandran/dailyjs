---
layout: post
title: "Backbone.js Tutorial: Updates for 1.0, Clear Complete"
author: Alex Young
categories: 
- backbone.js
- mvc
- node
- backgoog
- bootstrap
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
  <li><a href="http://dailyjs.com/2013/03/28/backbone-tutorial-15/"><strong>Part 15: Updates for 1.0, Clear Complete</strong></a></li>
</ul>

###Preparation

Before starting this tutorial, you'll need the following:

* [alexyoung / dailyjs-backbone-tutorial](https://github.com/alexyoung/dailyjs-backbone-tutorial) at commit `711c9f6`
* The API key from part 2
* The "Client ID" key from part 2
* Update `app/js/config.js` with your keys (if you've checked out my source)

To check out the source, run the following commands (or use a suitable Git GUI tool):

{% highlight text %}
git clone git@github.com:alexyoung/dailyjs-backbone-tutorial.git
cd dailyjs-backbone-tutorial
git reset --hard 711c9f6
{% endhighlight %}

###Updating to Backbone 1.0

I updated bTask to work with Backbone 1.0, which required two small changes.  The first was a change to the behaviour of callbacks in `Backbone.sync` -- the internal call to the `success` callback now only needs one argument, which is the response data.  I think I've mentioned that on DailyJS before, but you shouldn't need to worry about this in your own Backbone projects unless you've written a custom `Backbone.sync` implementation.

The second change was the collection `add` events were firing when the views called `fetch`.  I fixed this by passing `reset: true` to the `fetch` options.  Details on this have been included in [Backbone's documentation](http://backbonejs.org/) under "Upgrading to 1.0":

> If you want to smartly update the contents of a Collection, adding new models, removing missing ones, and merging those already present, you now call `set` (previously named "update"), a similar operation to calling `set` on a Model. This is now the default when you call `fetch` on a collection. To get the old behavior, pass `{reset: true}`.

###Adding "Clear Complete"

When a task in Google Tasks is marked as done, it will appear with strike-through and hang around in the list until it is cleared or deleted.  Most Google Tasks clients will have a button that says "Clear Complete", so I added one to bTask.

I added a method called `clear` to the `Tasks` collection which calls the `.clear` method from the Google Tasks API (rather than going through `Backbone.sync`):

{% highlight javascript %}
define(['models/task'], function(Task) {
  var Tasks = Backbone.Collection.extend({
    model: Task,
    url: 'tasks',

    clear: function(tasklist, options) {
      var success = options.success || function() {}
        , request
        , self = this
        ;

      options.success = function() {
        self.remove(self.filter(function(task) {
          return task.get('status') === 'completed';
        }));

        success();
      };

      request = gapi.client.tasks.tasks.clear({ tasklist: tasklist });
      Backbone.gapiRequest(request, 'update', this, options);
    }
  });

  return Tasks;
});
{% endhighlight %}

I also added a button (using Bootstrap's built-in icons) to `app/js/templates/app.html`, and added an event to `AppView` (in `app/js/views/app.js`):

{% highlight javascript %}
var AppView = Backbone.View.extend({
  // ...
  events: {
    'click .clear-complete': 'clearComplete'
  },

  // ...
  clearComplete: function() {
    var list = bTask.views.activeListMenuItem.model;
    bTask.collections.tasks.clear(list.get('id'), { success: function() {
      // Show some kind of user feedback
    }});
    return false;
  }
});
{% endhighlight %}

I had to change `app/js/views/lists/menuitem.js` to set the current collection in the `open` method to make this work.

###Summary

Because I've been reviewing Backbone's evolution as it progressed to 1.0 for DailyJS, updating this project wasn't too much effort.  In general the 1.0 release is backwards compatible, so you should definitely consider upgrading your own projects.  Also, now bTask has 'Clear Complete', I feel like it does enough of the standard Google Tasks features for me to actually use it regularly.

Remember that you can try it out for yourself at [todo.dailyjs.com](http://todo.dailyjs.com/).

The full source for this tutorial can be found in [alexyoung / dailyjs-backbone-tutorial, commit 705bcb4](https://github.com/alexyoung/dailyjs-backbone-tutorial/commit/705bcb4cd27d1794e52291e3c2d20e72a3b56022).
