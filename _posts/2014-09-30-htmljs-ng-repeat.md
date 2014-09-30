---
layout: post
title: "HTMLjs, Building an Angular List"
author: "Alex Young"
categories:
- angularjs
- libraries
- html
- mvvm
---

###HTMLjs

[HTMLjs](http://nhanaswigs.github.io/htmljs/api/index.html) (GitHub: [nhanaswigs / htmljs](https://github.com/nhanaswigs/htmljs), License: _MIT_) by Nhan Nguyen is a data-binding and template rendering library.  It supports browsers back to IE7.  Rather than using declarative HTML, it's more JavaScript-driven.  For example, given a simple `input` field, you could bind a validation handler to it like this:

{% highlight javascript %}
var username = html.data('')
  .required('Username is required.')
  .maxLength(15, 'Max length for username is 15 characters.');

html('#username').input(username);
{% endhighlight %}

I don't think declarative templates are a bad thing, but the detail most people consistently get wrong with Knockout is incorrectly binding prototype methods or values.  This API circumvents that by relying on simpler markup.  The author has provided [lots of examples](http://nhanaswigs.github.io/htmljs/api/index.html) so you can get a feel for how it works without downloading it.

###Building an Angular List: Using ng-repeat

[Building an Angular List: Using ng-repeat](http://randomjavascript.blogspot.co.uk/2014/09/building-angular-list-using-ng-repeat.html) is a tutorial by David Posin about how to use `ng-repeat`.  It's a simple introductory tutorial, and David includes a screencast so you can see exactly how it works.

I noticed David uses the web-based [Cloud9 IDE](https://c9.io/), so you can even follow along without installing anything if you're really new to Angular.
