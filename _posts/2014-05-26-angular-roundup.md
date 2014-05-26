---
layout: post
title: "ngActivityIndicator, angular-cog, dijs"
author: Alex Young
categories:
- angularjs
- di
- ajax
---

###ngActivityIndicator

![ngActivityIndicator](/images/posts/ngactivity.gif)

[ngActivityIndicator](http://labs.voronianski.com/ngActivityIndicator.js/) (GitHub: [voronianski / ngActivityIndicator](https://github.com/voronianski/ngActivityIndicator), License: _MIT_) by Dmitri Voronianski is an Angular provider for loading indicators, which you can use on directives, controllers or services.

Adding an indicator to a controller looks like this:

{% highlight javascript %}
var app = angular.module('exampleApp', ['ngActivityIndicator']);

app.controller('MainCtrl', ['$activityIndicator', '$timeout',
  function ($actvityIndicator, $timeout) {
    $actvityIndicator.startAnimating();
    $timeout(function () {
      $actvityIndicator.stopAnimating();
    }, 3000);
  }
]);
{% endhighlight %}

There's a directive called `ng-activity-indicator` which can be used to inject the indicator into the DOM automatically.

###angular-cog

angular-cog (GitHub: [chinmaymk / angular-cog](https://github.com/chinmaymk/angular-cog), License: _MIT_) by Chinmay Kulkarni is a library for writing declarative Ajax requests with Angular.

The full set of directives are as follows:

{% highlight html %}
<div cog-verb="{url}" 
        cog-model="{ng-model}" 
        cog-success="{angular.expression}" 
        cog-error="{angular.expression}"
        cog-trigger="{angular.expression}"
        cog-no-spinner="{true|false}" 
        cog-absolute-url="{true|false}" 
        cog-config="{object}">
</div>
{% endhighlight %}

Requesting JSON content should place it in the `$data` variable, so you can access it in `cog-success` and then pass it to something bound in `$scope`.

The documentation includes notes on how to set up a loading indicator -- maybe you could try ngActivityIndicator?

###dijs

dijs (GitHub: [cmtt / dijs](https://github.com/cmtt/dijs), License: _WTFPL_) by Matthias Thoemmes is a dependency injection module for Node and browsers that's inspired by Angular.  There are methods for defining a namespace, describing the modules, and resolving dependencies.

For describing dependencies, it supports function notation and array notation:

{% highlight javascript %}
// Function notation
var mod = Di();
mod.provide('Pi', Math.PI, true);
mod.provide('2Pi', function(Pi) { return 2*Pi; });

// Array notation
var mod = Di();
mod.provide('Math.Pi', Math.PI, true);
mod.provide('2Pi', ['Math.Pi', function (Pi) {
  return function () {
    return 2*Pi;
  };
}]);
{% endhighlight %}

There's a lot more to it than this, and you might find it useful if you've got used to DI through Angular but want to use it elsewhere.
