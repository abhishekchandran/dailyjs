---
layout: post
title: "Node Roundup: browser-perf, node-modules, module.exports vs. exports"
author: "Alex Young"
categories:
- node
- modules
- npm
---

###browser-perf

browser-perf (GitHub: [axemclion / browser-perf](https://github.com/axemclion/browser-perf), License: _BSD-2 Clause_, npm: [browser-perf](https://www.npmjs.org/package/browser-perf)) by Parashuram Narasimhan is a Node-based browser performance testing tool.  It collects various metrics from browsers and then displays graphs using the results.

It runs as a command-line script which allows you to specify which browsers you'd like to use:

{% highlight text %}
browser-perf http://example.com --browsers=chrome,firefox --selenium=ondemand.saucelabs.com --username=username --accesskey=accesskey
{% endhighlight %}

There's also a Node API:

{% highlight javascript %}
var browserPerf = require('browser-perf');
browserPerf('http://example.com/test', function(err, res) {
  // res - array of objects. Metrics for this URL
  if (err) {
    console.log('ERROR: ' + err);
  } else {
    console.log(res);
  }
}, {
  selenium: 'http://localhost:4444/wd/hub',
  browsers: ['chrome', 'firefox']
  username: SAUCE_USERNAME
});
{% endhighlight %}

There's a [wiki page with more details](https://github.com/axemclion/browser-perf/wiki/Node-Module---API).

The author has also written a [blog post about browser-perf](http://blog.nparashuram.com/2014/06/perfslides-demo-app-to-show-that.html) with a screenshot.

###node-modules.com

Gregor Elke sent in [node-modules.com](http://node-modules.com/), an alternative search engine for npm.  It was created by Mathias Buus Madsen and Tobias Baunbæk, and supports GitHub sign in for customisation.  It only requires access to your public details, and seems to sort results fairly well.

###module.exports vs. exports

Cho S. Kim sent in a post about [understanding module.exports and exports](http://www.choskim.me/understanding-module-exports-and-exports-in-node-js/):

> A module encapsulates related code into a single unit of code. When creating a module, this can be interpreted as moving all related functions into a file.
> The keyword require returns an object, which references the value of `module.exports` for a given file. If a developer unintentionally or intentionally re-assigns `module.exports` to a different object or different data structure, then any properties added to the original `module.exports` object will be unaccessible.


