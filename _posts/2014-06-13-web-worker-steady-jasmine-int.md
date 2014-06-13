---
layout: post
title: "Web Worker Contest, Steady.js, Jasmine Integration Tests"
author: "Alex Young"
categories:
- jasmine
- testing
- webworker
- ui
---

###Web Worker Contest

The [Web Worker Contest](http://www.webworkercontest.net/), sent in by Stefan Trenkel, is a JavaScript game where two programs compete to conquer a two-dimensional space using simple movement commands.

> On a playing area of 100 x 100 square fields two JavaScript programs compete against each other. From a randomly allotted starting point they must conquer as many fields as possible. The winner is who occupies most fields at the end. A move is to conquer from the current field either the upper, lower, right or left adjacent field. The new field can be occupied only if it was not previously occupied by the opponent's program. If a move is possible (the new field is free) the current position changes to the desired field. If a move is not possible (the field is occupied by the opponent or you want to leave the playing area), you stay on the current position. Fields that one has previously occupied can be used again (but do not count double). The programs do not have any information about the playing area.

The contest is based on the Web Worker API:

> Your own Web Worker is simply a local JavaScript file with appropriate code. In this case your own Web Worker is not uploaded to the server. This option is primarily for testing and optimizing your own Web Worker. If you want to participate in the WWC you have to upload your Worker on the Upload page.

You can view [running games](http://www.webworkercontest.net/game.php) and read more about the concept in the [guide](http://www.webworkercontest.net/guide.php).

###Steady.js

[Steady.js](http://lafikl.github.io/steady.js/) (GitHub: [lafikl / steady.js](https://github.com/lafikl/Steady.js), License: _MIT_) by Khalid Lafi is a library for elegantly responding to `onscroll` events.  With Steady.js, the `onscroll` handler collects data, then offloads the work to `requestAnimationFrame`.  It throttles events, and works like `@media-query`.

Steady.js is based around "trackers": these provide the logic that the data collector uses.  An example of a built-in tracker is `scrollTop` which indicates how far a scrollable element has moved from the top.

Basic usage looks like this:

{% highlight javascript %}
var s = new Steady({
  conditions: {
    width: 400,
    scrollX: 0,
    max-bottom: 200
  },
  throttle: 100,
  handler: fn
});

s.addCondition('scrollX', 0);
{% endhighlight %}

The documentation has an example of a custom tracker that you can extend with your own behaviour.

###Jasmine Integration Tests

[jasmine-integration](https://github.com/jordinl/jasmine-integration) by Jordi Noguera is an integration testing extension for Jasmine.  It allows you to run tests in browsers by using an `iframe`, or in headless mode using PhantomJS.

The documentation shows how to use it with Grunt, so you can execute your tests against a browser with `grunt jasmine:server`, or in headless mode using `grunt jasmine:server:ci`.

Jordi has written a sample app with tests called [node-todo](https://github.com/jordinl/node-todo) which demonstrates how the same specs can be used for browser testing and headless tests on the command-line.

