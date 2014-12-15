---
layout: post
title: "Survey Closed, Predicates, Shackles"
author: "Alex Young"
categories:
- surveys
- modules
- libraries
- assert
---

###Survey Closed

The [JavaScript Developer Survey 2014](http://dailyjs.com/2014/12/01/javascript-survey/) has now closed.  I received some updates for the survey to the [GitHub repository](https://github.com/alexyoung/dailyjs-survey/), so you should see those the next time I run it.  Thanks for the contributions!

I'll work on writing up the results and post again when they're ready.

###Predicates

Predicates (GitHub: [wookieb/predicates](https://github.com/wookieb/predicates), License: _MIT_, npm: [predicates](https://www.npmjs.org/package/predicates)) by Łukasz Kużyński is a set of tools for type checking and assertions.  For example:

{% highlight javascript %}
var is = require('predicates');

is.string(1); // false
is.string('test'); // true
is.undefinedOr(is.string, undefined); // true
{% endhighlight %}

Assertions look like this:

{% highlight javascript %}
var assertName = createAssert(is.string, 'Name must be a string');

var Person = function(name, surname, age) {
  assertName(name);
  assertSurname(surname);
  assertAge(age);
}

new Person('Tom', 'Welling', 33); // OK!
{% endhighlight %}

The [Predicates API guide](https://github.com/wookieb/predicates/blob/master/docs/api.md) has a list of each available method, and there's also an interesting [API design document](https://github.com/wookieb/predicates/blob/master/docs/design.md) that provides some background to the project.

###Shackles

Shackles (GitHub: [metaraine/shackles](https://github.com/metaraine/shackles), License: _ISC_, npm: [shackles](https://www.npmjs.com/package/shackles)) by Raine Lourie is a module for adding chaining to another library.  Imagine if Underscore didn't support chaining.  You could use Shackles to create a fluent API, like this:

{% highlight javascript %}
var chain = shackles(_);

var result = chain([1,2,3])
  .map(function (x) { return x*x })
  .filter(function (x) { return x > 2 })
  .value(); // [4,9]
{% endhighlight %}

You can insert values at any point in the chain with `tap`, and there's also a `log` method that prints values with `console`.  Logging can be overridden as well.
