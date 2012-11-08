---
layout: post
title: "AngularJS: Common Pitfalls"
author: "Alex Young"
categories: 
- mvc
- angularjs
- backbone.js
---

I noticed [this commit](https://github.com/angular/angular.js/commit/f4517b500c0d2357d89e8c889f32f1466e5c1612) to [AngularJS](http://angularjs.org/) by Braden Shepherdson that updates the [AngularJS FAQ](http://docs.angularjs.org/misc/faq) with a list of common pitfalls to avoid.  Some of these pieces of sage advice can be applied to other MVC frameworks like Backbone.js, or at least act as some inspiration:

> Stop trying to use jQuery to modify the DOM in controllers. Really. That includes adding elements, removing elements, retrieving their contents, showing and hiding them.

Similarly, the Backbone.js documentation advises the use of scoped DOM queries.  Also, [Backbone patterns](http://ricostacruz.com/backbone-patterns/) suggests ensuring event handlers are correctly abstracted rather than using jQuery event handlers outside of Backbone.js code.

> If you're struggling to break the habit, consider removing jQuery from your app.

This might seem drastic, but AngularJS packs in enough functionality to get by without jQuery for the most part.  The FAQ suggests using jQLite for binding to events.

> There's a good chance that your app isn't the first to require certain functionality. There are a few pieces of Angular that are particularly likely to be reimplemented out of old habits.

After this the author describes how to take advantage of `ng-repeat`, `ng-show`, and `ng-class`.  It's the kind of practical knowledge that comes from hard-won experience, but it's all explained quite clearly here.  For example, `ng-class` can accept objects, including conditional expressions:

{% highlight html %}
<div ng-class="{ errorClass: isError, warningClass: isWarning, okClass: !isError && !isWarning }">...</div>
{% endhighlight %}

Although AngularJS, Backbone.js, and Knockout all have great documentation, I feel like the learning curve once the basics have been mastered is pretty tough.  It's good to see these low-level tips cropping up to clarify how the authors intend the project to be used.
