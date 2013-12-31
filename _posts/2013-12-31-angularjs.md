---
layout: post
title: "AngularJS Roundup: ngDialog.js, ocLazyLoad, angular-validation"
author: "Alex Young"
categories: 
- angularjs
- validation
- CoffeeScript
- modal
- ui
---

People keep sending me AngularJS scripts to write about, so I've collected a few together to start a probably infrequent AngularJS Roundup.  This week we've got three scripts to talk about, and the first is ngDialog.js.

###ngDialog.js

[ngDialog.js](http://likeastore.github.io/ngDialog/) (GitHub: [likeastore / ngDialog](https://github.com/likeastore/ngDialog), License: _MIT_) by Dmitri Voronianski is a modal dialog and popover provider.  You can load it and display a dialog like this:

{% highlight javascript %}
var app = angular.module('exampleApp', ['ngDialog']);

app.controller('MainCtrl', function($scope, ngDialog) {
  $scope.clickToOpen = function () {
    ngDialog.open({ template: 'popupTmpl.html' });
  };
});
{% endhighlight %}

The markup for the dialog can be a string, or loaded from a template:

{% highlight html %}
<script type="text/ng-template" id="templateId">
  <h1>Template heading</h1>
  <p>Content goes here</p>
</script>
{% endhighlight %}

You can even use the `ng-dialog` directive.  The project comes with two default themes, and you can use one of those to get started creating your own.  The default theme has CSS animations and media queries.

###ocLazyLoad

[ocLazyLoad](http://blog.getelementsbyidea.com/load-a-module-on-demand-with-angularjs/) (GitHub: [ocombe / ocLazyLoad](https://github.com/ocombe/ocLazyLoad)) by Olivier Combe is a module for lazy loading dependencies in AngularJS.  It's a service provider that allows you to load files with promises, like this:

{% highlight javascript %}
$ocLazyLoad.load({
  name: 'TestModule',
  files: ['testModule.js']
}).then(function() {
  console.log('done');
});
{% endhighlight %}

The blog post explains how the whole thing works, with detailed examples and explanations of how AngularJS loads modules.

> Since the modules can only be loaded on startup and the application can only be launched using the `ng-app` directive, if we can find the app module, we can get the complete list of all loaded modules and dependencies.

###Angular Validation

[Angular Validation](http://huei90.github.io/angular-validation/) (GitHub: [huei90 / angular-validation](https://github.com/huei90/angular-validation)) by Huei Tan is a set of form validation directives.  It supports various validation methods -- watch, blur, or submit, so you can show errors when it makes sense for your application.

It has some built in validation types, but you can add your own in JavaScript by loading the `validation` provider, and then adding new validation "expressions".  Expressions are loaded based on the `validator` attribute.  The readme has an example of how to do this, with the `huei` validator.

###AngularJS with CoffeeScript

Finally, Elad Ossadon sent in an article about making AngularJS classes work better with CoffeeScript: [Angular.js CoffeeScript Controller Base Class](http://www.devign.me/angular-dot-js-coffeescript-controller-base-class/).

It's a fairly short post with a base class snippet and an example controller module.
