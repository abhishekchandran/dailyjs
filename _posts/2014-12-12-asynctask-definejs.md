---
layout: post
title: "AsyncTask, DefineJS ES6 Features"
author: "Alex Young"
categories:
- es6
- generators
- webworkers
---

###AsyncTask

[Web workers](https://developer.mozilla.org/en-US/docs/Web/Guide/Performance/Using_web_workers) are great, but who wants to go to the trouble of creating extra files just to run some code in parallel?  AsyncTask (GitHub: [gorillatron/async-task](https://github.com/gorillatron/async-task), License: _MIT_, npm: [async-task](https://www.npmjs.com/package/async-task)) by Jørn Andre Tangen is a more generic web worker constructor that lets you define background tasks purely with JavaScript:

{% highlight javascript %}
var task = new AsyncTask({
  doInBackground: function(a, b) {
    return a + b
  }
});

task.execute(1, 2)
  .then(function(result) {
    result === 3
  })
  .catch(handleException);
{% endhighlight %}

It has a fluent API, and has Karma/Mocha unit tests as well.

###DefineJS: ES6 Generator Syntax

Recently I wrote about Mehran Hatami's [define.js](https://github.com/fixjs/define.js) project, which is a lightweight AMD implementation.  It has just been updated to support ES6 generators for loading modules, which means you can do this:

{% highlight javascript %}
var module = yield require('module');
{% endhighlight %}

It's still asynchronous, but it looks synchronous.  I think this is a really cool use of generators, and apparently several people asked Mehran to implement this so it seems like there's demand for it.

