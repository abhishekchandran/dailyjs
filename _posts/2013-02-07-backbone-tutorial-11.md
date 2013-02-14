---
layout: post
title: "Backbone.js Tutorial: Spies, Stubs, and Mocks"
author: Alex Young
categories: 
- backbone.js
- mvc
- node
- backgoog
- testing
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
  <li><a href="http://dailyjs.com/2013/02/07/backbone-tutorial-11/"><strong>Part 11: Spies, Stubs, and Mocks</strong></a></li>
  <li><a href="http://dailyjs.com/2013/02/14/backbone-tutorial-12/">Part 12: Testing with Mocks</a></li>
</ul>

###Preparation

Before starting this tutorial, you'll need the following:

* [alexyoung / dailyjs-backbone-tutorial](https://github.com/alexyoung/dailyjs-backbone-tutorial) at commit `9691fc1`
* The API key from part 2
* The "Client ID" key from part 2
* Update `app/js/config.js` with your keys (if you've checked out my source)

To check out the source, run the following commands (or use a suitable Git GUI tool):

{% highlight text %}
git clone git@github.com:alexyoung/dailyjs-backbone-tutorial.git
cd dailyjs-backbone-tutorial
git reset --hard 9691fc1
{% endhighlight %}

###Testing Custom Backbone.Sync APIs

The goal of this tutorial is to demonstrate how to write tests so they don't need to use live APIs.  The way this is usually done is through a technique known as mocking -- when the application attempts to talk to the API, it will communicate with a special object that we can control.

When testing applications that revolve around a custom `Backbone.sync` implementation, you need to cleanly separate application testing from testing the remote API.  We just want to test what we're responsible for, and run tests without an Internet connection!  If you look at the way `app/js/gapi.js` works, it relies on `gapi.client` which is provided by Google.  This is an easy target for mocking -- we can replace Google's library with something that returns sample data instead.

[Sinon.JS](http://sinonjs.org/) does all of this, and more.  Sinon makes it easy to "spy" on the methods that would usually result from trying to connect to the remote server, and these spies can easily be plugged into suitable assertions.

The basic approach I employ for testing Backbone applications with Sinon is as follows:

* Create spies for CRUD operations
* Script the DOM to trigger the things I want to test
* Ensure the spies have seen the expected calls
* Check that the UI has been updated accordingly

Here's an example in our application:

* The user clicks 'Add List' and enters a list title
* The form is submitted
* Assert that `gapi.client.tasks.tasklists` has been called to _insert_ the new list
* Assert that a new list item has been added to the UI

In Mocha/Sinon, that could be expressed like this:

{% highlight javascript %}
suite('Lists', function() {
  var spyUpdate = sinon.spy(gapi.client.tasks.tasklists, 'update')
    , spyCreate = sinon.spy(gapi.client.tasks.tasklists, 'insert')
    , spyDelete = sinon.spy(gapi.client.tasks.tasklists, 'delete')
    ;

  setup(function() {
    spyUpdate.reset();
    spyCreate.reset();
  });

  test('Creating a list', function() {
    // TODO: Do the DOM stuff for creating a list
    assert.equal(1, spyCreate.callCount);
  });

  test('Editing a list', function() {
    // TODO: Do the DOM stuff for editing a list
    assert.equal(1, spyUpdate.callCount);
  });

  // Example: Abstraction for testing
  test('Deleting a list', function() {
    // TODO: Do the DOM stuff for deleting a list
  });
});
{% endhighlight %}

Save this as `test/lists.test.js` and add `lists.test.js` as a `script` tag to `test/index.html` (after `app.test.js`).

[Sinon spies](http://sinonjs.org/docs/#spies) are created with `sinon.spy()`.  In this example I've provided two arguments to `sinon.spy`, an object and a method.  This causes Sinon to replace the method with a wrapped version that can count the number of times it gets called.  It behaves like the original method, but makes testing things easier.

Spies can be invoked in other ways, but in this tutorial I'm just going to focus on this particular pattern.  In general this is the part of Sinon that I find myself using the most when it comes to testing Backbone applications.

###Housekeeping

In my quest to keep these tutorials clear and simple, I noticed I made some changes to the app which caused the tests to break.  That means you'll need to do a bit of housekeeping to get the tests to work correctly.

First, let's get the application views loaded inside a container instead of overwriting the entire `body`.  Mocha needs a `div` to display test results, and the last version of the app caused it to be overwritten when the tests urn.

Add a new `div` to `app/index.html` and `test/index.html` just after the `body` opening tag:

{% highlight html %}
<div id="todo-app"></div>
{% endhighlight %}

You can hide this `div` in the tests if you like, setting `display: none` won't break anything.  This change also requires that `app/js/views/app.js` is updated to use `#todo-app` instead of `body` for the `el` property (near the top of the file).

You'll also need to add some new `script` tags to `test/index.html`:

{% highlight html %}
<script src="lib/sinon.js"></script>
<script src="fixtures/gapi.js"></script>
{% endhighlight %}

There's one thing left to do in `test/index.html` -- change the way the Mocha tests are invoked at the bottom of the file:

{% highlight html %}
<script>
  // Only run the tests when the application is ready
  require(['app'], function() {
    bTask.apiManager.on('ready', function() { mocha.run(); });
  });
</script>
{% endhighlight %}

This is a good way to make sure the tests run only when the application's dependencies have all loaded and have been evaluated.

###Download Sinon.JS

This is the version of Sinon.JS that I've used: [sinon-1.5.2.js](http://sinonjs.org/releases/sinon-1.5.2.js).  Save it to `test/lib` and create the `lib/` directory if it doesn't already exist.

###Mocking Google's API

To mock Google's API, I've simply overwritten the library it provides with my own object that runs the expected callbacks with suitable test data.  I created this test data by using the app and looking at the Network tab in WebKit Inspector, so it's based on a subset of my actual to-do lists and tasks.

You can use my test data if you want to follow this tutorial instead of checking out the full source from GitHub: [alexyoung/4730178 (gapi.js)](https://gist.github.com/alexyoung/4730178).

Save it to `test/fixtures/gapi.js`, creating the directory if required.

Now when `app/js/gapi.js` calls `gapi.client.load` and logs in with OAuth2, it'll actually receive fake user data.  I've used similar data structures to real values, but I've removed a few things like etags to make it easier to read.

###Testing Lists

Now `test/lists.test.js` can be finished off.  Here's one way to test that lists are created correctly:

{% highlight javascript %}
test('Creating a list', function() {
  var $el = bTask.views.app.$el
    , listName = 'Example list';

  // Show the add list form
  $el.find('#add-list-button').click();

  // Fill out a value for the new list's title
  $el.find('#list_title').val(listName);
  $el.find('#list_title').parents('form').first().submit();

  // Make sure the spy has seen a call for a list being created
  assert.equal(1, spyCreate.callCount);

  // Ensure the expected UI element has been added
  assert.equal(listName, $('.list-menu-item:last').text().trim());
});
{% endhighlight %}

This test uses jQuery to click the button that opens the list add/edit form, then fills out a title, and subsequently submits the form.  That will cause `Backbone.sync` to run, and call an `insert` operation from Google's API.  Because I've replaced `gapi` it will call the fixture instead, and since Sinon is spying on it we'll get an incremented call count.  Boom!

Editing a list is practically the same:

{% highlight javascript %}
test('Editing a list', function() {
  var $el = bTask.views.app.$el;

  // Show the edit list form
  $el.find('.list-menu-item:first').click();
  $el.find('#edit-list-button').click();

  $el.find('#list_title').val('Edited list');
  $el.find('#list_title').parents('form').first().submit();

  assert.equal(1, spyUpdate.callCount);
  assert.equal('Edited list', $('.list-menu-item:first').text().trim());
});
{% endhighlight %}

This time an `update` API call will fire rather than an `insert`.

There is one curious wrinkle in these tests -- handling delete.  I've used a `confirm` dialog instead of a fancy modern modal widget, which means the tests will cause a `confirm` dialog to appear.  It's possible to stop the dialog from appearing by replacing `confirm`:

{% highlight javascript %}
test('Deleting a list', function() {
  var $el = bTask.views.app.$el;

  // Automatically accept the confirmation
  window.confirm = function() { return true; };

  // Show the edit list form
  $el.find('#edit-list-button').click();

  // Click the list delete button
  $el.find('.delete-list').click();

  assert.equal(1, spyDelete.callCount);
});
{% endhighlight %}

The problem with this is it'll cause Mocha to see a "global leak".  You can add `confirm` to `test/setup.js` to prevent that error.  However, ideally we shouldn't need to do this -- coupling tests to implementation details like this is usually a bad idea.  It would be better to design the application to allow the dialog to be turned off to better support testing.  I don't usually mind adapting applications to make them easier to test, it can be beneficial in the long run.

To run these tests, launch the Node app with `npm start` and then visit `http://localhost:8080/test/` in your browser.  Make sure you type the URL correctly or the tests won't work due to the use of relative paths.

###Summary

In this part you've seen how to write tests for an application based around a custom `Backbone.sync` implementation.  Sinon spies provide the perfect way to wrap internal parts of a Backbone application to write succinct test suites.

This particular type of testing focuses on the business logic represented by Backbone models, collections, and views.  This ultimately helps in maintaining your client-side applications as they grow and change over time.

The majority of the source for this tutorial can be found in [alexyoung / dailyjs-backbone-tutorial, commit 5b0a529](https://github.com/alexyoung/dailyjs-backbone-tutorial/commit/5b0a5298f6ebf39e2cfd7304e77a702e335d21fa).  The final commit was [45dd59](https://github.com/alexyoung/dailyjs-backbone-tutorial/tree/45dd59179bb0b5ef5eb2de769e3ec940c5828366).
