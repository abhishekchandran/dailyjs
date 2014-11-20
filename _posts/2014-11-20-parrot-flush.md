---
layout: post
title: "Parrot, Flush Timeouts"
author: "Alex Young"
image: "/images/posts/parrotlogo.png"
categories:
- timers
- api
- libraries
- modules
---

###Parrot

Parrot (GitHub: [sailorjs/parrotjs](https://github.com/sailorjs/parrotjs), License: _MIT_, Bower: _parrotjs_) by Kiko Beats is a library for wrapping API calls to your server.  You can register different environments, which makes it easy to switch between development and production.  You can also register URLs with different protocols, so it's possible to make WebSocket or Ajax requests.

It has a fluent API, so you can chain calls.  If you wanted to register your production and development servers, then you'd call `endpoint.add`:

{% highlight javascript %}
parrot.endpoint
  .add(name: 'development', url: 'http://localhost:3000')
  .add(name: 'production', url: 'http://example.com')
{% endhighlight %}

Specific API URLs can be added as well:

{% highlight javascript %}
parrot.url
  .add(name: 'signup', path: 'user', method: 'post')
  .add(name: 'login', path: 'user/login', method: 'post');
{% endhighlight %}

Making an Ajax request to the signup route would just be `parrot.ajax('signup', function(err, res) {`.

This seems preferable to some client-side HTTP APIs.  The author intended it to be used with [Sails.js](http://sailsjs.org/#/), but you could use it with other frameworks as well.

###flush-timeouts

I've noticed a few libraries recently that aim to improve the JavaScript timer API.  Alex Lawrence sent in flush-timeout (GitHub: [efacilitation/flush-timeouts](https://github.com/efacilitation/flush-timeouts), License: _MIT_, Bower: _flush-timeouts_, npm: [flush-timeouts](https://www.npmjs.org/package/flush-timeouts)), a module for overriding `setTimeout`.

Here's a quick example:

{% highlight javascript %}
require('flush-timeouts');

var i = 0;

function demo() {
  console.log('i:', i);
  i++;
}

setTimeout(demo, 500);
setTimeout(demo, 1000);
setTimeout(demo, 1500);

global.flushTimeouts();

console.log('Done');
{% endhighlight %}

This will cause `demo` to immediately run three times, and then print `Done`.  If you removed `global.flushTimeouts` then it would execute based on the delays passed to `setTimeout`.

flush-timeouts might be useful when you're trying to queue up tasks with `setTimeout` but have additional logic that determines if it's safe to run all the tasks at once.  Or perhaps you've got tests for code that depends on `setTimeout` and don't want to wait.  The author has supplied tests and build scripts so you can pick it apart to see how it works.
