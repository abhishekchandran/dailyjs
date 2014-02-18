---
layout: post
title: "AngularJS Infinite Scroll, Bindable.js"
author: Alex Young
categories:
- dom
- angularjs
- data-binding
---

###AngularJS Infinite Scroll

This project made me wonder if AngularJS modules are the new jQuery plugins: [lrInfiniteScroll](http://lorenzofox3.github.io/lrInfiniteScroll/) (GitHub: [lorenzofox3 / lrInfiniteScroll](https://github.com/lorenzofox3/lrInfiniteScroll), License: _MIT_), by Laurent Renard.  It's a small and highly reusable library that is specifically tailored to work well with Angular's API.

It attaches an event handler to an element that fires when the element has been scrolled to the bottom.  You can use it to automatically load items on demand, Angular style:

{% highlight html %}
<ul lr-infinite-scroll="myEventHandler" scroll-threshold="200" time-threshold="600">
  <li ng-repeat="item in myCollection">
</ul>
{% endhighlight %}

###Bindable.js

Data binding libraries are often coupled to view objects.  Bindable.js (GitHub: [classdojo / bindable.js](https://github.com/classdojo/bindable.js), License: _MIT_) from ClassDojo (and Craig Condon) is a more generic bidirectional data binding library.  Bindable objects are constructed, and then properties can be bound to callbacks:

{% highlight javascript %}
var person = new bindable.Object({
  name: 'craig',
  last: 'condon',
  location: {
    city: 'San Francisco'
  }
});

person.bind('location.zip', function(value) {
  // 94102
}).now();

// Triggers the binding
person.set('location.zip', '94102'); 
{% endhighlight %}

Bindable objects emit other events (change, watching, dispose), and there are methods for introspection (`bindable.has`), context (`bindable.context`), and triggering callbacks after they're defined (`.now`).
