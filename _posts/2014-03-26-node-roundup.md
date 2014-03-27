---
layout: post
title: "Node Roundup: npm Search Ranking, shortest-route, prova"
author: Alex Young
categories:
- node
- npm
- modules
- testing
---

###npm Search Ranking

<div class="image">
  <img src="/images/posts/npmsearch-mar-2014.png" />
  <small>Improved search results.</small>
</div>

[npm's search results are now ranked by popularity](http://blog.npmjs.org/post/80789086446/nicer-perusal-method):

> Packages are now scored by a nifty new algorithm that takes into account the package's popularity (i.e. number of stars and average weekly downloads over a month). The algorithm also does some proper word parsing (so you can actually find "socket.io" with the search "socket io") and gives higher weight to things that match the search query in the package name and details.

The interface has been tweaked as well, so you can easily see how many downloads and starts a project has.

I was sceptical about the quality of the results, but I've recently been researching material for my book so I've been searching npm a lot, and generic searches now seem to get more useful results.

###shortest-route

Shortest-route (GitHub: [tarun29061990 / shortest-route](https://github.com/tarun29061990/shortest-route), License: _ISC_, npm: [shortest-route](https://www.npmjs.org/package/shortest-route)) by Tarun Chaudhary is a [travelling salesman problem](http://en.wikipedia.org/wiki/Travelling_salesman_problem) solver that you can install with npm.

It calculates the distance between cities using the [Google Distance Matrix API](https://developers.google.com/maps/documentation/distancematrix/), and accepts city descriptions as a pipe-separated list:

{% highlight javascript %}
var shortestRoute = require('shortest-route');

shortestRoute.getShortPath('A|B|C', function(json) {
  console.log('data='+json);
});
{% endhighlight %}

Although you probably won't need this for a project any time soon, I like the fact a hard problem is installable with npm.  For more details, [see Tarun's blog post](http://activegeek22.wordpress.com/2014/03/18/my-efforts-to-solve-travelling-salesman-problem-through-javascript/).

###prova

<div class="image">
  <img src="/images/posts/prova-djs.gif" />
  <small>Automatically running tests when files change.</small>
</div>

I like [tape](https://github.com/substack/tape) by Substack -- it's easy to read and produces flexible test output.  Azer also likes it, so he wrote prova (GitHub: [azer / prova](https://github.com/azer/prova), License: _GPL_, npm: [prova](https://www.npmjs.org/package/prova)), a Node and browser test runner based on tape and browserify.

It has a built-in web application that uses [watchify](https://github.com/substack/watchify) to automatically run tests when files change.  That means you can edit code and see live results in a browser.

