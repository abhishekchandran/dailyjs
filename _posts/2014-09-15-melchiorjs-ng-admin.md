---
layout: post
title: "Melchior.js, ng-admin"
author: "Alex Young"
categories:
- libraries
- modules
- angularjs
- ui
---

###Melchior.js

[Melchior.js](http://labs.voronianski.com/melchior.js/) (GitHub: [voronianski / melchior.js](https://github.com/voronianski/melchior.js), License: _MIT_, npm: [melchiorjs](https://www.npmjs.org/package/melchiorjs)) by Dmitri Voronianski is an implementation of the [Chainable Module Definition](https://github.com/tjwudi/wd.js/wiki/module-loader) concept introduced by John Wu.

>The idea behind chainable modules solves several nasty AMD patterns like long lines of declaring dependencies and provides simplicity and readability with its' visual-friendly and clean syntax.
>
>As CommonJS is more good for non-browser environments, chaining modules with requires fit perfectly for in-browser use cases.

Here's an example of the API:

{% highlight javascript %}
// create module
melchiorjs.module('yourModule')

// define dependencies
.require('dependencyUno')
.require('dependencyDuo', 'duo')

// define module body
.body(function () {
  // `dependencyUno` is available here!
  dependencyUno.doSomething();

  // aliased `dependencyDuo` is available as `duo`!
  duo.doSomething();

  // return methods for other modules
  return {
    method: function () { ... },
    anotherMethod: function () { ... }
  };
});
{% endhighlight %}

The readme has more examples including one for AngularJS.  This API does seem more idiomatic than most module loaders, so it'll be interesting to see if it catches on.

###ng-admin

François Zaninotto sent in [ng-admin](http://marmelab.com/blog/2014/09/15/easy-backend-for-your-restful-api.html) (GitHub: [marmelab / ng-admin](https://github.com/marmelab/ng-admin), License: _MIT_), a cool project that adds an administration interface to RESTful CRUD APIs.

There's a [demo on Amazon](http://ec2-54-194-84-85.eu-west-1.compute.amazonaws.com/#/dashboard) and documentation that shows how to configure ng-admin to use your application's entities.  It copes with field mappings, and references.  References can be 1-N, N-1, and many to many.

François suggests that ng-admin is useful because if you're creating a lot of projects with different backends (MongoDB, MySQL, Node, Python) you can still add a platform-agnostic administration UI.

The same authors also made [gremlins.js](https://github.com/marmelab/gremlins.js).
