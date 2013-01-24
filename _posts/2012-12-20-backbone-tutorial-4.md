---
layout: post
title: "Backbone.js Tutorial: Backbone.sync"
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
  <li><a href="http://dailyjs.com/2012/12/20/backbone-tutorial-4/"><strong>Part 4: Backbone.sync</strong></a></li>
  <li><a href="http://dailyjs.com/2012/12/27/backbone-tutorial-5/">Part 5: List Views</a></li>
  <li><a href="http://dailyjs.com/2013/01/03/backbone-tutorial-6/">Part 6: Creating Lists</a></li>
  <li><a href="http://dailyjs.com/2013/01/10/backbone-tutorial-7/">Part 7: Editing Lists</a></li>
  <li><a href="http://dailyjs.com/2013/01/17/backbone-tutorial-8/">Part 8: Deleting Lists</a></li>
  <li><a href="http://dailyjs.com/2013/01/24/backbone-tutorial-9/">Part 9: Tasks</a></li>
</ul>

###Preparation

Before starting this tutorial, you'll need the following:

* [alexyoung / dailyjs-backbone-tutorial](https://github.com/alexyoung/dailyjs-backbone-tutorial) at commit `c1d5a2e7cc`
* The API key from part 2
* The "Client ID" key from part 2
* Update `app/js/config.js` with your keys (if you've checked out my source)

To check out the source, run the following commands (or use a suitable Git GUI tool):

{% highlight text %}
git clone git@github.com:alexyoung/dailyjs-backbone-tutorial.git
cd dailyjs-backbone-tutorial
git reset --hard c1d5a2e7cc
{% endhighlight %}

###Google's Tasks API

To recap: the point of this tutorial series is to build a Backbone.js single page application that uses client-side JavaScript to communicate with Google's authentication and to-do list APIs.  Got that?  Good!

Google provides access to our to-do lists through two APIs:

* [Tasklists](https://developers.google.com/google-apps/tasks/v1/reference/tasklists#resource)
* [Tasks](https://developers.google.com/google-apps/tasks/v1/reference/tasks)

When loading Google's JavaScript, the browser is bestowed with a global called `gapi` that provides access to various objects and methods.  In the last part, I quietly included a call to `gapi.client.load` that loads the `tasks` API:

{% highlight javascript %}
gapi.client.load('tasks', 'v1', function() { /* Loaded */ });
{% endhighlight %}

This can be found in `app/js/gapi.js`.  The remaining challenge before building the interface is to implement a new `Backbone.sync` method that uses `gapi` to communicate with the Tasks and Tasklists APIs.

###Backbone.sync Structure

I've already talked about the overall structure of `Backbone.sync` in [part 2](http://dailyjs.com/2012/12/06/backbone-tutorial-2/).  The pattern I'll use in these tutorials is fairly generic, so you could use the same approach to communicate with something other than Google's APIs.

The `sync` method itself takes three arguments, the first of which is the `method` (`create`, `update`, `delete`, and `read`).  We need to map `method` to something Google's API can understand.

This is what we've got so far:

{% highlight javascript %}
Backbone.sync = function(method, model, options) {
  options || (options = {});

  switch (method) {
    case 'create':
    break;

    case 'update':
    break;

    case 'delete':
    break;

    case 'read':
    break;
  }
};
{% endhighlight %}

Google's Tasks API methods map to the Backbone `method` argument like this:

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

Even though Google's API doesn't look like the Rails 3-based RESTful API that Backbone.js is designed for out of the box, it's still very close.

###Making Requests with `gapi`

The `gapi` object makes requests using this pattern:

* Call one of the `gapi.client.tasks` methods with the _request content_ to get a `request` object
* Call `request.execute` with a callback to send the request
* The callback receives a `response` object, much like a standard Ajax request

Here's what this looks like in reality:

{% highlight javascript %}
var requestContent = {}
  , request
  , gapiResource;

gapiResource = 'tasks';
requestContent['tasklist'] = tasklistId; // Assuming we have one
requestContent['resource'] = model.toJSON();

// 'insert' is for creating new tasks
request = gapi.client.tasks[gapiResource].insert(requestContent);

// Send the request to the API
request.execute(function(res) {
  // Handle the response
});
{% endhighlight %}

Looking at this, it's clear that we need two models: `Task` and `TaskList`.  There also need to be two corresponding collections: `Tasks` and `TaskLists`.

Backbone models and collections have URLs -- these are used for making API requests.  Similarly, Google's APIs have URLs: `tasks` and `tasklists`, so by using the model URL `Backbone.sync` can determine which API resource is required for a given request.

###Models

Create a new directory called `app/js/models` and add `task.js`:

{% highlight javascript %}
define(function() {
  var Task = Backbone.Model.extend({
    url: 'tasks'
  });

  return Task;
});
{% endhighlight %}

You'll also want to create a `app/js/models/tasklist.js`:

{% highlight javascript %}
define(function() {
  var TaskList = Backbone.Model.extend({
    url: 'tasklists'
  });

  return TaskList;
});
{% endhighlight %}

###Collections

Create another new directory called `app/js/collections` and add `tasklists.js`:

{% highlight javascript %}
define(['models/tasklist'], function(TaskList) {
  var TaskLists = Backbone.Collection.extend({
    model: TaskList
  , url: 'tasklists'
  });

  return TaskLists;
});
{% endhighlight %}

We're going to use the `TaskList` collection later on to load your task lists.

###Making API Requests

Open up `app/js/gapi.js` and add a new line after line 36:

{% highlight javascript %}
app.views.auth.$el.hide();
$('#signed-in-container').show();
self.trigger('ready'); // This one
{% endhighlight %}

This `'ready'` event will be used to signify that authentication was successful, and the Tasks API is ready for use.  Next, add the following two lines to `Backbone.sync`, inside the `read` switch case:

{% highlight javascript %}
case 'read':
  var request = gapi.client.tasks[model.url].list(options.data);
  Backbone.gapiRequest(request, method, model, options);
break;
{% endhighlight %}

This code creates a request, and then `Backbone.gapiRequest` will execute it and delegate the response.

Here's the most basic `Backbone.gapiRequest` implementation:

{% highlight javascript %}
Backbone.gapiRequest = function(request, method, model, options) {
  var result;
  request.execute(function(res) {
    if (res.error) {
      if (options.error) options.error(res);
    } else if (options.success) {
      result = res.items;
      options.success(result, true, request);
    }
  });
};
{% endhighlight %}

All it does is run `request.execute`, which is provided by Google, and then maps the result to be compatible with Backbone's API by running the `success` and `error` callbacks.

Just so you can see something is really happening, open `app/js/app.js` and make it load the `TaskLists` collection by changing the `define` invocation at the top:

{% highlight javascript %}
define([
  'gapi'
, 'views/app'
, 'views/auth'
, 'collections/tasklists'
],

function(ApiManager, AppView, AuthView, TaskLists) {
{% endhighlight %}

Now add this to the `connectGapi` method:

{% highlight javascript %}
this.apiManager.on('ready', function() {
  self.collections.lists.fetch({ data: { userId: '@me' }, success: function(res) {
    _.each(res.models, function(model) {
      console.log(model.get('title'));
    });
  }});
});
{% endhighlight %}

That code uses Underscore's `each` method to iterate over each "model" returned by `Backbone.sync`, which is called by the `TaskList` collection.

Run the server with `npm start`, and visit `http://localhost:8080`.  If you run it in a browser that supports `console`, then you should see your task lists printed out.

<div class="image">
  <img src="/images/posts/backbone-tutorial-api-example.png" alt="" />
  <small>My task lists.</small>
</div>

If you've got this working then you're not far off building a real world Backbone.js app that communicates with Google's APIs.  The same concepts can be applied to other Google JavaScript APIs.

###Summary

The full source for this tutorial can be found in [alexyoung / dailyjs-backbone-tutorial, commit fcd653ec6](https://github.com/alexyoung/dailyjs-backbone-tutorial/tree/fcd653ec6fa5916246e3f8b9b5f942f4be31d2e7).

