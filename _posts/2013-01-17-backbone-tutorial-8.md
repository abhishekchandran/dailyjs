---
layout: post
title: "Backbone.js Tutorial: Deleting Lists"
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
  <li><a href="http://dailyjs.com/2013/01/17/backbone-tutorial-8/"><strong>Part 8: Deleting Lists</strong></a></li>
  <li><a href="http://dailyjs.com/2013/01/24/backbone-tutorial-9/">Part 9: Tasks</a></li>
  <li><a href="http://dailyjs.com/2013/01/31/backbone-tutorial-10/">Part 10: Oh No Not More Tasks</a></li>
  <li><a href="http://dailyjs.com/2013/02/07/backbone-tutorial-11/">Part 11: Spies, Stubs, and Mocks</a></li>
  <li><a href="http://dailyjs.com/2013/02/14/backbone-tutorial-12/">Part 12: Testing with Mocks</a></li>
</ul>

###Preparation

Before starting this tutorial, you'll need the following:

* [alexyoung / dailyjs-backbone-tutorial](https://github.com/alexyoung/dailyjs-backbone-tutorial) at commit `0953c5d`
* The API key from part 2
* The "Client ID" key from part 2
* Update `app/js/config.js` with your keys (if you've checked out my source)

To check out the source, run the following commands (or use a suitable Git GUI tool):

{% highlight text %}
git clone git@github.com:alexyoung/dailyjs-backbone-tutorial.git
cd dailyjs-backbone-tutorial
git reset --hard 0953c5d
{% endhighlight %}

###Deleting Lists

We're now at the end of the complete CRUD implementation for lists.  To support deleting items, we just need to hook up the link that we've already added and add support for the `delete` method to `gapi.js`.  You could try doing this yourself for practice.

Open `app/js/views/app.js`, and add an event binding for the "Delete List" link:

{% highlight javascript %}
events: {
  'click #add-list-button': 'addList'
, 'click #edit-list-button': 'editList'
, 'click #delete-list-button': 'deleteList'
},
{% endhighlight %}

Next, add a method called `deleteList` to the same class:

{% highlight javascript %}
deleteList: function() {
  if (confirm('Are you sure you want to delete that list?')) {
    bTask.views.activeListMenuItem.model.destroy();
  }
  return false;
}
{% endhighlight %}

Just by making those two changes, the active list will be removed from the interface.  Backbone knows how to remove the view when `model.destroy` is called in `deleteList`.

###Backbone.sync Changes

To persist deleting lists, open `app/js/gapi.js` and add a `case` for `'delete'` after `'update'` (it should be around line 100):

{% highlight javascript %}
case 'delete':
  requestContent['resource'] = model.toJSON();
  request = gapi.client.tasks[model.url].delete(requestContent);
  Backbone.gapiRequest(request, method, model, options);
break;
{% endhighlight %}

Google's API provides the `delete` method, otherwise this is identical to the implementation for updating items.

###Next

This part was short, so consider this your week off.  Go and play with the source and see what you can get the Google Tasks API and Backbone to do!  There's still a lot of things left to cover, however.

Over the last eight weeks you've learned how to:

* Write a custom `Backbone.sync` method
* Use the [Google Task API](https://developers.google.com/google-apps/tasks/) with client-side JavaScript
* Write Backbone models, views, and collections

This could be adapted to work with other Google APIs, or potentially even other APIs that I haven't considered.  Once you have a solid understanding of how Backbone models and syncing data works, then a lot becomes possible.

The next few parts will cover the following:

* Mocking the Google Tasks API for testing
* Adding, editing, and deleting the tasks themselves
* A Bootstrap user interface
* Customising Bootstrap

###Summary

The full source for this tutorial can be found in [alexyoung / dailyjs-backbone-tutorial, commit 8d88095](https://github.com/alexyoung/dailyjs-backbone-tutorial/tree/8d88095de512c084ccf4cb28e49844df05396e0f).

