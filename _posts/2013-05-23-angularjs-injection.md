---
layout: post
title: "AngularJS: More on Dependency Injection"
author: Alex Young
categories: 
- angularjs
- mvc
- angularfeeds
---

In the [AngularJS tutorials](http://dailyjs.com/tags#angularfeeds) I've been writing, you might have noticed the use of dependency injection.  In this article I'm going to explain how dependency injection works, and how it relates to the small tutorial project we've created.

Dependency injection is a software design pattern.  The motivation for using it in Angular is to make it easier to transparently load mocked objects in tests.  The `$http` module is a great example of this: when writing tests you don't want to make real network calls, but defer the work to a fake object that responds with fixture data.

The earlier tutorials used dependency injection for this exact use case: in [main controller](https://github.com/alexyoung/djsreader/blob/c9f9d06258f4973018a1cc48c226642bbb32938f/app/scripts/controllers/main.js#L3-L4), the `MainCtrl` module is set up to load the `$http` module which can then be transparently replaced during testing.

{% highlight javascript %}
angular.module('djsreaderApp')
  .controller('MainCtrl', function($scope, $http, $timeout) {
{% endhighlight %}

Now forget everything I just said about dependency injection, and look at the callback that has been passed to `.controller` in the previous example.  The `$http` and `$timeout` modules have been added by me because I want to use the [$http service](http://docs.angularjs.org/api/ng.$http) and the [$timeout service](http://docs.angularjs.org/api/ng.$timeout).  These are built-in "services" (an Angular term), but they're not standard arguments.  In fact, I could have specified these arguments in any order:

{% highlight javascript %}
angular.module('djsreaderApp')
  .controller('MainCtrl', function($scope, $timeout, $http) {
{% endhighlight %}

This is possible because Angular looks at the function argument _names_ to load dependencies.  Before you run away screaming about magic, it's important to realise that this is just one way to load dependencies in Angular projects.  For example, this is equivalent:

{% highlight javascript %}
angular.module('djsreaderApp')
  .controller('MainCtrl', ['$scope', '$http', '$timeout'], function($scope, $http, $timeout) {
{% endhighlight %}

The array-based style is more like [AMD](https://github.com/amdjs/amdjs-api/wiki/AMD), and requires a little bit of syntactical overhead.  I call the first style "introspective dependency injection".  The array-based syntax allows us to use different names for the dependencies, which can be useful sometimes.

This raises the question: how does introspective dependency injection cope with minimisers, where variables are renamed to shorter values?  Well, it doesn't cope with it at all.  In fact, minimisers need help to translate the first style to the second.

###Yeoman and ngmin

One reason I built the tutorial series with [Yeoman](http://yeoman.io/) was because the Angular generator includes [grunt-ngmin](https://github.com/btford/grunt-ngmin).  This is a [Grunt](http://gruntjs.com/) task that uses [ngmin](https://github.com/btford/ngmin) -- an Angular-aware "pre-minifier".  It allows you to use the shorter, introspective dependency injection syntax, while still generating valid minimised production builds.

Therefore, building a production version of [djsreader](https://github.com/alexyoung/djsreader) with `grunt build` will correctly generate a deployable version of the project.

Why is it that almost all of Angular's documentation and tutorials include the potentially dangerous introspective dependency injection syntax?  I'm not sure, and I haven't looked into it.  I'd be happier if the only valid solution was the array-based approach, which looks more like AMD which most of us are already comfortable with anyway.

Just to prove I'm not making things up, here is the minimised source for djsreader:

{% highlight javascript %}
"use strict";angular.module("djsreaderApp",[]).config(["$routeProvider",function(e){e.when("/",{templateUrl:"views/main.html",controller:"MainCtrl"}).otherwise({redirectTo:"/"})}]),angular.module("djsreaderApp").controller("MainCtrl",["$scope","$http","$timeout",function(e,r,t){e.refreshInterval=60,e.feeds=[{url:"http://dailyjs.com/atom.xml"}],e.fetchFeed=function(n){n.items=[];var o="http://query.yahooapis.com/v1/public/yql?q=select%20*%20from%20xml%20where%20url%3D'";o+=encodeURIComponent(n.url),o+="'%20and%20itemPath%3D'feed.entry'&format=json&diagnostics=true&callback=JSON_CALLBACK",r.jsonp(o).success(function(e){e.query.results&&(n.items=e.query.results.entry)}).error(function(e){console.error("Error fetching feed:",e)}),t(function(){e.fetchFeed(n)},1e3*e.refreshInterval)},e.addFeed=function(r){e.feeds.push(r),e.fetchFeed(r),e.newFeed={}},e.deleteFeed=function(r){e.feeds.splice(e.feeds.indexOf(r),1)},e.fetchFeed(e.feeds[0])}]);
{% endhighlight %}

The demangled version shows that we're using the array-based syntax, thanks to ngmin:

{% highlight javascript %}
angular.module("djsreaderApp").controller("MainCtrl", ["$scope", "$http", "$timeout",
{% endhighlight %}

###Internals

In case you're wondering how the introspective dependency injection style works, then look no further than [annotate(fn)](https://github.com/angular/angular.js/blob/0272240400d7896224f34b9f10b492994e29c655/src/auto/injector.js#L45-L71).  This function uses `Function.prototype.toString` to extract the argument names from the JavaScript source code.  The results are effectively cached, so even though this sounds horrible it doesn't perform as badly as it could.

###Conclusion

Nothing I've said here is new -- while researching this post I found [The Magic Behind Dependency Injection](http://www.alexrothenberg.com/2013/02/11/the-magic-behind-angularjs-dependency-injection.html) by Alex Rothenberg, which covers the same topic, and the [Angular Dependency Injection documentation](http://docs.angularjs.org/guide/di) outlines the issues caused by the introspective approach and suggests that it should only be used for [pretotyping](http://www.pretotyping.org/).

However, I felt like it was worth writing an overview of the matter, because although Yeoman is great for a quick start to a project, you really need to understand what's going on behind the scenes!
