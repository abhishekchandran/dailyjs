---
layout: post
title: "Backbone Directives"
author: "Alex Young"
categories:
- backbone
- angularjs
- libraries
---

Tal Bereznitskey writes:

> This is an open source project to enrich Backbone.js with AngularJS style directives.
>
>  I used to hear people talk about the new hotness and I didn't really want to let go of Backbone. I took quick looks from time to time and found some stuff I didn't like in AngularJS.
>
> The DOM was filled with things like "ng-click" which reminded me of the spaghetti age of HTML and JavaScript.

When I first started using Angular I also found custom attributes (directives) concerning.  However, after using them I realised that they can really help make code more declarative and concise.  Tal came to the same conclusion, and created [Backbone Directives](http://berzniz.github.io/backbone.directives/example/index.html) (GitHub: [berzniz / backbone.directives](https://github.com/berzniz/backbone.directives), License: _MIT_) to bring the same pattern to Backbone projects.

It includes things like `bb-bind` which implements data-binding with expression support, and `bb-class` for changing an element's class.

Expressions use the same code as [Angular's expression parser](https://github.com/angular/angular.js/blob/f09b6aa5b58c090e3b8f8811fb7735e38d4b7623/src/ng/parse.js), which attempts to safely execute JavaScript by using a sandbox that prevents access to certain properties (like `.constructor`).

{% highlight javascript %}
// Sandboxing Angular Expressions
// ------------------------------
// Angular expressions are generally considered safe because these expressions only have direct
// access to $scope and locals. However, one can obtain the ability to execute arbitrary JS code by
// obtaining a reference to native JS functions such as the Function constructor.
{% endhighlight %}

Not all data binding libraries support expressions as well as this, so Tal has opted to fork Angular's approach so you can get the same functionality in your Backbone applications.

Tal wrote a [post about the project](http://berzniz.com/post/93498862096/give-your-backbone-js-apps-super-powers-with-angularjs), with his thoughts on Angular, Backbone, and how to use Backbone Directives.
