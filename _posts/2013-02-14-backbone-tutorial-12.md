---
layout: post
title: "Backbone.js Tutorial: Testing with Mocks"
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
  <li><a href="http://dailyjs.com/2013/02/07/backbone-tutorial-11/">Part 11: Spies, Stubs, and Mocks</a></li>
  <li><a href="http://dailyjs.com/2013/02/14/backbone-tutorial-12/"><strong>Part 12: Testing with Mocks</strong></a></li>
  <li><a href="http://dailyjs.com/2013/03/07/backbone-tutorial-13/">Part 13: Routes</a></li>
  <li><a href="http://dailyjs.com/2013/03/14/backbone-tutorial-14/">Part 14: Customosing the UI</a></li>
</ul>

###Preparation

Before starting this tutorial, you'll need the following:

* [alexyoung / dailyjs-backbone-tutorial](https://github.com/alexyoung/dailyjs-backbone-tutorial) at commit `5b0a529`
* The API key from part 2
* The "Client ID" key from part 2
* Update `app/js/config.js` with your keys (if you've checked out my source)

To check out the source, run the following commands (or use a suitable Git GUI tool):

{% highlight text %}
git clone git@github.com:alexyoung/dailyjs-backbone-tutorial.git
cd dailyjs-backbone-tutorial
git reset --hard 5b0a529
{% endhighlight %}

###Mocks

Last week I wrote about testing a custom `Backbone.sync` implementation using Sinon's spies.  This worked well in our situation where the transport layer isn't necessarily pinned down -- Sinon includes [Fake XMLHttpRequest](http://sinonjs.org/docs/#server), but this won't work with Google's API as far as I know.  This week I want to introduce another testing concept that Sinon provides: mocks.

Mocks are fake methods that allow expectations to be registered.  Historically, you'll find mocks being used in unit tests where I/O occurs.  If you're testing business logic you don't need to check if a file was written or a network call was made, it's often preferable to attach an expectation to make sure the appropriate API _would have_ been called.

In Sinon, creating a mock returns an object that can be decorated with expectations.  The API is chainable, so it's low on boilerplate and high on readability.  What you're aiming to do is state "whenever this method is called, ensure it was called with these parameters".  This can be done through mocks by setting up expectations using matchers.

[Matchers](http://sinonjs.org/docs/#sinon-match-api) are similar to assertions -- they can be used to check that arguments are everything from primitive types to instances of a constructor, or even literal values.

Last week we used spies to ensure Google's API was accessed in the expected way.  Mocks could be used for this as well.  We don't really care about the request so much as the fact a particular CRUD operation was requested.  The signature for `Backbone.gapiRequest` is `request, method, model, options` -- the `method` argument is generally what we're interested in.  Therefore, to set up an expectation that saving an existing task caused `update` to fire, we can use a mock with `sinon.match.object`:

{% highlight javascript %}
var mock = sinon.mock(Backbone);
mock.expects('gapiRequest').once().withArgs(sinon.match.object, 'update');

// Do UI stuff to cause the task to be edited and the form to be submitted
mock.verify();
{% endhighlight %}

###Mocks Compared to Spies

The previous example looked a lot like last week's spies, and using spies for the same thing used less code.  So, when should we use mocks, and when should we use spies?  Mocks give you a fine-grained control over the order and behaviour of method calls.  Spies have a different API which focuses on checking how callbacks or methods are used.  If you were testing a method that accepts a callback, you could pass in a spy to see how the callback gets used.  With a mock, the callback would be from the system under test, and you'd set up expectations on it.

When it comes to UI testing -- triggering interface actions to invoke code, I find it's easier to treat the entire Backbone stack as a whole and use spies to ensure the expected behaviour occurs.  Rather than writing a test for each model, view, and collection, it makes more sense to drive the UI and hook into model or sync operations to verify the outcome.

In last week's tests where lists were being tested, I probably wouldn't use mocks because mocks should have a closer relationship to a given method under test.  The kinds of tests we're writing involve more than one method, so spies and assertions on the DOM make more sense.

###Mock Example

A good place to use mocks is for testing `app/js/gapi.js`.  Let's say we're interested in making sure `gapiRequest` gets called by `Backbone.sync`.  We could use mocks:

{% highlight javascript %}
test('gapiRequest is called by Backbone.sync', function() {
  var mock = sinon.mock(Backbone);
  mock.expects('gapiRequest').once();
  Backbone.sync('update', model, {});
  mock.verify();
});
{% endhighlight %}

This calls `Backbone.sync` to cause `gapiRequest` to be called once.  This test doesn't verify the behaviour of `gapiRequest` itself, just the fact it gets called.

One quirk of the custom `Backbone.sync` API is `Task.prototype.get` is called twice: once to fetch task's ID, and another to get the list's ID.  We could test this with mocks if it was deemed important:

{% highlight javascript %}
test('Ensure Task.prototype.get is called twice', function() {
  var mock = sinon.mock(model);

  mock.expects('get').twice().returns(model.id);
  Backbone.sync('update', model);
  mock.verify();
});
{% endhighlight %}

This uses the `twice` expectation with another mock.

Hopefully you're starting to understand how mocks and spies differ.  There's another major part of Sinon, though, and that's the stub API.

###Stubs

Digging further into `Backbone.gapiRequest`, requests are expected to have an `execute` method which gets called to send data to Google's API.  Both spies and stubs can be used to test this using the `yieldsTo` method:

{% highlight javascript %}
test('gapiRequest causes the execute callback to fire', function() {
  var spy = sinon.spy();
  sinon.stub(Backbone, 'gapiRequest').yieldsTo('execute', spy);
  Backbone.sync('update', model);

  assert.ok(spy.calledOnce);
  Backbone.gapiRequest.restore();
});
{% endhighlight %}

This test causes the following chain of events to occur:

1. `Backbone.sync` calls `Backbone.gapiRequest`
2. `Backbone.gapiRequest` receives an object with an `execute` property, which we've replaced with a spy
3. `Backbone.gapiRequest` calls this execute method, therefore satisfying `assert.ok(spy.calledOnce)`

Putting these ideas together can be used to make sure the right `success` or `error` callbacks are triggered after a request has completed:

{% highlight javascript %}
test('Errors get called', function() {
  var spy = sinon.spy()
    , options = { error: spy }
    ;

  // Stub the internal update method that would usually come from Google
  sinon.stub(gapi.client.tasks.tasks, 'update').returns({
    execute: sinon.stub().yields(options)
  });

  // Invoke a sync with a fake model and the options with the error callback
  Backbone.sync('update', model, options);

  assert.ok(spy.calledOnce);
  gapi.client.tasks.tasks.update.restore();
});
{% endhighlight %}

This test makes sure `error` gets called by using a spy, and it also stubs out `gapi.client.tasks.tasks.update` with our own object.  This object has an `execute` property which causes the callback inside `gapiRequest` to run, and ultimately call `error`.

###Clearing Up

I've written a test suite for tasks.  It's based on last week's tests so there isn't really anything new, apart from the `teardown` method:

{% highlight javascript %}
setup(function() {
  /// ...

  spyUpdate = sinon.spy(gapi.client.tasks.tasks, 'update')
  spyCreate = sinon.spy(gapi.client.tasks.tasks, 'insert')
  spyDelete = sinon.spy(gapi.client.tasks.tasks, 'delete')

  // ...
});

teardown(function() {
  gapi.client.tasks.tasks.update.restore();
  gapi.client.tasks.tasks.insert.restore();
  gapi.client.tasks.tasks.delete.restore();
});
{% endhighlight %}

I've found this pattern is better than calling `reset`, because it's easy to attempt to wrap objects more than once when multiple test files are loaded.

###Writing Good Tests with Sinon

Sinon might look like a small library that you can drop into Mocha, Jasmine, or QUnit, but there's an art to writing good Sinon tests.  Sinon's documentation has some explanation of when exactly spies, mocks, and stubs are useful, but there is a subjective factor at play particularly when it comes to deciding whether a test is best written with a mock or a stub.

A few tips I've found useful are:

* Spies are great for the times when you want to test the entire application, rather than a specific class or method
* Stubs come in handy when there are methods you don't want run or want to force execution down a given path
* Mocks are good for testing specific methods
* A single mock per test case should be used
* You should use `restore()` after using spies and stubs, it's easy to forget and causes "double wrap" errors

###Summary

Stylistically spies, stubs, and mocks are very different, but they're vexingly similar until you've had some practice with Sinon.  There have been mock vs. stub discussions on the [Sinon.JS Google Group](http://groups.google.com/group/sinonjs), so it's probably best to ask Christian on that group if you're struggling get Sinon to do what you want.

The source for this tutorial can be found in [alexyoung / dailyjs-backbone-tutorial, commit 0c6de32](https://github.com/alexyoung/dailyjs-backbone-tutorial/tree/0c6de32aec7513027908a5877c1c346b059a36a2).
