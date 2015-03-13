---
layout: post
title: "Prüfer, Calendar Base"
author: Alex Young
categories:
- dom
- modules
- node
- testing
- calendar
---

### Prüfer

Johnathan Leppert wanted a way to generate complex DOM structures for UI performance testing.  He decided to use the [Prüfer sequence](http://en.wikipedia.org/wiki/Pr%C3%BCfer_sequence), and created a Node module that can generate random trees of data (GitHub: [jleppert/prufer](https://github.com/jleppert/prufer), License: _MIT_).

Here's an example of the usage:

{% highlight javascript %}
var prufer = require('prufer');

// to make a tree, supply a series of integers
var tree = prufer([3, 3, 3, 4]);

// you'll get back an array of edges
console.log(tree);
{% endhighlight %}

I thought the Prüfer sequence sounded like a cool way to do this -- it might be useful for lots of Node-related stream tools.

###Calendar Base

Wesley de Souza sent in a module for generating calendars as arrays of objects.  The module is called Calendar Base (GitHub: [WesleydeSouza/calendar-base](https://github.com/WesleydeSouza/calendar-base), License: _MIT_, npm: [calendar-base](https://www.npmjs.com/package/calendar-base)).  To use it, you just need to instantiate a new calendar:

{% highlight javascript %}
var cal = new Calendar({ siblingMonths: true });
cal.getCalendar(2015, 5);
{% endhighlight %}

The arrays it generates have objects like this: `{ day: 31, weekDay: 0, month: 4, year: 2015, siblingMonth: true }`.  It also has methods for changing the start date, and selecting the current date.

It reminds me of typing `cal` in Unix, which is still how I use calendars instead of using a fancy desktop application...
