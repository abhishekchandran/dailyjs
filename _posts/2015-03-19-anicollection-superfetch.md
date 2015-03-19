---
layout: post
title: "AniCollection, SuperFetch"
author: Alex Young
image: "/images/posts/anicss.png"
categories:
- node
- modules
- libraries
- css
- animation
- http
---

### AniCollection

I usually write CSS animations by failing to remember the syntax and then copy and pasting examples until it works the way I want.  In times like that a handy directory of CSS animations is essential.  [AniCollection](http://anicollection.github.io/#/) (GitHub: [anicollection/anicollection](https://github.com/anicollection/anicollection/), License: _MIT_) by Dariel Noel is big collection of CSS animations.  Each animation has a preview and the associated CSS in an easy copy and pastable format.

![AniCollection](/images/posts/anicss.png)

The site itself is on GitHub, and the author has built it with Grunt, [css-annotation](https://www.npmjs.com/package/css-annotation), and [js-beautify](https://www.npmjs.com/package/js-beautify).

### SuperFetch

I actually like the [request module's API](http://npmjs.com/package/request), but juggling multiple requests can be awkward.  SuperFetch (GitHub: [luin/superfetch](https://github.com/luin/superfetch), License: _MIT_, npm: [superfetch](https://www.npmjs.com/package/superfetch)) by Zihua Li is a promise-based HTTP API that is built on request:

{% highlight javascript %}
var fetch = require('superfetch');
fetch.get('http://example.com').then(function(body) {
  // when the status code begins with "2", the response body will be returned.
}).catch(function(response) {
  // otherwise, the whole response(including headers) is returned.
});
{% endhighlight %}

You can use `fetch.get.option` to set options, and you can chain calls to `option` if you like.  The request and response objects can be transformed with callbacks, and the author has included unit tests written with Mocha.
