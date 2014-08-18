---
layout: post
title: "PerfBar, ngAtp"
author: "Alex Young"
categories:
- libraries
- ui
- angularjs
- performance
- benchmarks
---

###PerfBar

![PerfBar](/images/posts/perfbar.png)

[PerfBar](http://lafikl.github.io/perfBar/) (GitHub: [lafikl / perfBar](https://github.com/lafikl/perfBar), License: _MIT_) by Khalid Lafi is a script that adds various benchmarks to a page.  To use it, add `perfBar.js` and then configure some metrics:

{% highlight javascript %}
perfBar.init({
  budget: {
    'loadTime': {
      max: 200
    },
    'redirectCount': {
      max: 1
    },
    'globalJS': {
      min: 2,
      max: 5
    }
  }
});
{% endhighlight %}

You can use `perfBar.enable` and `perfBar.disable` to toggle metrics.  [The documentation](http://lafikl.github.io/perfBar/) has PerfBar included on the page so you can see what it looks like, and each of the available metrics is documented.

Some of the available metrics are the total number of DOM elements, the time for the DOM content to load, request duration, and backend/frontend processing time.

###ngAtp

[ngAtp](http://yiransheng.github.io/ngAtp/) (GitHub: [yiransheng / ngAtp](https://github.com/yiransheng/ngAtp), License: _MIT_, Bower: `ng-atp`) by Yiran Sheng is an autocompletion library for AngularJS.  The basic usage is to specify the `ng-atp` and `ng-atp-config` directives.  The config option uses a [Bloodhound](https://github.com/twitter/typeahead.js/blob/master/doc/bloodhound.md) config object, which comes from Twitter's typeahead.js suggestion engine.

In ngAtp, Bloodhound is included as an Angular service, with Angular's `$http` library instead of `jQuery.ajax`.  It reuses Bloodhound, so you get features like prefetching, intelligent caching, fast lookups, and backfilling, but with an Angular-friendly API.
