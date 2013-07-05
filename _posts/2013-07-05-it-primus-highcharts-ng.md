---
layout: post
title: "Primus, it.js, highcharts-ng"
Author: Alex Young
categories:
- node
- functional
- graphs
- libraries
- AngularJS
---

###Primus

![Primus](/images/posts/primus.png)

[Primus](https://medium.com/the-build/22af5c94a922) (GitHub: [3rd-Eden / primus](https://github.com/3rd-Eden/primus), License: _MIT_, npm: [primus](https://npmjs.org/package/primus)) by Arnout Kazemier is a wrapper for various popular real-time frameworks.  It allows you to switch between SocketJS, Engine.IO, or Socket.IO.

> The biggest problems always happen when you deploy your application to production servers. This is when they receive large quantities of traffic and small bugs can lead to major disasters. Wouldn't it be nice to be able to switch between real-time servers when they are the source of your issues without having to rewrite your application?

It includes client-side hooks, so both your Node and browser-based code can be written independent of the underlying communication layer.  The APIs are event-based, and documentation and tests have been included.

###it.js

it.js (GitHub: [dtinth / it.js](https://github.com/dtinth/it.js), License: _MIT_, npm: [it.js](https://npmjs.org/package/it.js)) by Thai Pangsakulyanont is a small functional library inspired by [Q](https://github.com/kriskowal/q) and [Underscore](http://underscorejs.org/) for creating accessor and iterator callbacks.  It's chainable, which means you can do this:

{% highlight javascript %}
It.get('first').get('length')
{% endhighlight %}

Instead of this:

{% highlight javascript %}
function(person) { return person.first.length; }
{% endhighlight %}

Wrappers for boolean operators have been included, so your chains can include logic:

{% highlight javascript %}
// these three are equivalent to function(x) { return !x.last }
console.log(_.select(addressBook, It.not(It.get('last'))));
console.log(_.select(addressBook, It.get('last').not()));
console.log(_.select(addressBook, It.not('last')));
{% endhighlight %}

###highcharts-ng

highcharts-ng (GitHub: [pablojim / highcharts-ng](https://github.com/pablojim/highcharts-ng), License: _MIT_) by Barry Fitzgerald is an AngularJS directive for [Highcharts](http://www.highcharts.com/).  Barry says this demonstrates how easy it is to use third-party JavaScript with AngularJS.  He's posted an [example on jsFiddle](http://jsfiddle.net/pablojim/Cp73s/).

Here's a snippet of how it looks just so you can see that it looks like idiomatic AngularJS code:

{% highlight javascript %}
var myapp = angular.module('myapp', ['highcharts-ng']);

myapp.controller('myctrl', function($scope) {
  $scope.addPoints = function() {
    var seriesArray = $scope.chart.series
    var rndIdx = Math.floor(Math.random() * seriesArray.length);
    seriesArray[rndIdx].data = seriesArray[rndIdx].data.concat([1, 10, 20]);
  };
{% endhighlight %}
