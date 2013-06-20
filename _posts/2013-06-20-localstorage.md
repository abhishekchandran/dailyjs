---
layout: post
title: "MV* and Local Storage"
author: Alex Young
categories:
- frameworks
- mv*
- localStorage
---

Most AngularJS and Backbone.js projects that I've worked on have persisted data to a remote API.  What about those times when storing data in the browser is sufficient?  Enterprising developers have added support for `localStorage` to some MVC frameworks, but before dropping one of these plugins or libraries into your project you need to know a little background about the API and its limitations.

###Browser Support

If you're already set on building a modern, single page web application, legacy browser support probably isn't a huge deal.  The [Can I use Web Storage](http://caniuse.com/namevalue-storage) page shows most browsers we typically target are supported.  It refers to "name/value pairs" because it's talking about the `localStorage` API.

###The `localStorage` API

If you've never used it before, then you can think of `window.localStorage` as a key/value store for strings.  You can stick any JavaScript value you like in there, but a string will be returned on retrieval.

{% highlight javascript %}
window.localStorage.setItem('age', 18);
window.localStorage.getItem('age');
// "18"
{% endhighlight %}

This means you should think carefully about what data you store.  Aspirations of creating a browser-based Photoshop backed by `localStorage` isn't architecturally sensible -- it would be nice if binary data could be stored, but for now you'll have to make do with strings.

The storage limit in most browsers is 5 MB, which probably doesn't sound like much, but it's actually [1000 times more](http://en.wikipedia.org/wiki/Web_storage) than is supported by cookies.

###AngularJS

There are examples of apps that use `localStorage` on the [AngularJS blog](http://blog.angularjs.org/).  One that I downloaded and picked apart was [FoodMe](https://github.com/IgorMinar/foodme) by Igor Minar.  In FoodMe, Igor creates a [localStorage](https://github.com/IgorMinar/foodme/blob/master/app/js/services/localStorage.js) service which basically just wraps `window.localStorage` so it can be loaded with dependency injection.  The `$scope` is then watched, and a string version of a given record is dumped into `localStorage` using `JSON.stringify`:

{% highlight javascript %}
foodMeApp.factory('customer', function($rootScope, localStorage) {
  var LOCAL_STORAGE_ID = 'fmCustomer';
  var customerString = localStorage[LOCAL_STORAGE_ID];

  var customer = customerString ? JSON.parse(customerString) : {
    name: undefined,
    address: undefined
  };

  $rootScope.$watch(function() { return customer; }, function() {
    localStorage[LOCAL_STORAGE_ID] = JSON.stringify(customer);
  }, true);

  return customer;
});
{% endhighlight %}

The record is loaded from `localStorage`, and serialised using `JSON.parse` and `JSON.stringify`.  Notice that Igor has used the object-style API: `localStorage.setItem(key, value)` and `localStorage[key] = value` are equivalent.

###Backbone.js

Jerome Gravel-Niquet created Backbone.localStorage (GitHub: [jeromegn / Backbone.localStorage](https://github.com/jeromegn/Backbone.localStorage), License: _MIT_, bower: _backbone.localStorage_), which allows collections to store data with `localStorage`.  It's a drop-in solution -- barely any configuration is required.  All you need to do is add a `localStorage` property to your collection classes.

Backbone.localStorage has tests, and the author is still updating it.  GitHub currently lists 31 contributors.

###Knockout

This isn't meant to be an exhaustive review of `localStorage` libraries, but I thought I'd also mention [Knockout](http://knockoutjs.com/).  knockout.localStorage (GitHub: [jimrhoskins / knockout.localStorage](https://github.com/jimrhoskins/knockout.localStorage)) by Jim Hoskins makes `ko.observable` and `ko.observableArray` objects able to persist data to `localStorage`.  You'll need to specify a `persist` property which includes the key to store the observable's data under.

It's not quite as well-maintained or tested as Backbone.localStorage, but it does the job.  There are some open pull requests that add things like [AMD support](https://github.com/jimrhoskins/knockout.localStorage/pull/5).

###Events

The Web Storage specification also defines a ["storage" event](http://www.w3.org/TR/webstorage/#the-storage-event).  It fires when data changes, but you can't stop it unlike other DOM events.  This might make a more convenient bridge to data-binding frameworks.

###Sync

If you've made an amazing single page app that persists data to `localStorage`, and you're interested in adding a server-side API so users can save and sync data, what do you do?  Well, step back and redefine the problem.  Since `localStorage` is limited in size, why not use it like a caching layer?  Your application could store data locally _until_ a server is available, which suits a lot of use-cases, including mobile deployment.  This is exactly what [Backbone Caching Sync](https://github.com/ggozad/Backbone.cachingSync) by Yiorgis Gozadinos does.

###Cache

Another use people have found for `localStorage` is caching client-side _assets_.  One example of this is [basket.js](http://addyosmani.github.io/basket.js/) by Addy Osmani.

> Bing and Google Search make extensive use of localStorage for stashing SCRIPT blocks that are used on subsequent page views. None of the other top sites from my previous post use localStorage in this way. Are Bing and Google Search onto something? Yes, definitely.

###Summary

If you need to persist data, `localStorage` can slot into data-binding and MVC/MVVC frameworks rather nicely.  There are libraries out there, but with `JSON.parse` and `JSON.stringify` it's trivial to store data.  For applications with a server, then `localStorage` can be used as a temporary cache, which has the added benefit of helping support devices with intermittent network access.
