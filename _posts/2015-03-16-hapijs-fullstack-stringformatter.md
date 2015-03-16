---
layout: post
title: "StringFormatter, Hapi.js in Action, FullStack 2015"
image: "/images/posts/hapiaction.jpg"
author: Alex Young
categories:
- libraries
- strings
- books
- conferences
- events
---

###StringFormatter

Simon Blackwell sent me StringFormatter (GitHub: [anywhichway/stringformatter](https://github.com/anywhichway/stringformatter), License: _MIT_), a string formatting library that aims to go beyond the new ECMAScript string templates.  It's a bit like `sprintf` formatting, but includes some more complex features:

* Numerical type formatting
* Date formatting
* CSS styles
* Conditional formatting
* Caching

It can handle expressions like currency as well, which is ideal for web applications when you want to display multiple currency formats.  You can use `StringFormatter.register` to register a formatting for a type.  For example, if you had a date formatter object you could associate it with `Date` like this: `StringFormatter.register(Date, dateFormatter, 'Date')`.

The usual way to format a string is with `StringFormatter.format`, but you can use `StringFormatter.polyfill()` to add string formatting to the `String` object.  Format strings are represented with JavaScript-inspired syntax:

{% highlight javascript %}
StringFormatter.format(
  "The time is now {Date: {format:'hh:mm'}} and I have {number: {fixed: 2, currency: '$'}}.",
  new Date('2015-03-13T10:01:27.284Z'),
  50.25
);
{% endhighlight %}

All format options accept an additional `style` string, which causes the output to be wrapped in `span` elements with inline styles.

Ideally this library should be used with a templating system to really cut down on format invocation boilerplate.  Simon has included an example for the [Ractive](http://www.ractivejs.org) template engine.

###Hapi.js in Action

![Hapi in Action](/images/posts/hapiaction.jpg)

[Hapi.js in Action](http://manning.com/harrison/) by Matt Harrison is a book that's dedicated to web development with [Hapi.js](http://hapijs.com).  It has been released as an early access edition, and pricing starts at $35.99 for the eBook.  The planned content includes authentication, building modular applications with plugins, testing, production, proxies, and creating streaming services.

> Hapi.js in Action teaches you how to build modern Node-driven applications using Hapi.js. Packed with examples, this book takes you from your first simple server through the skills you'll need to build a complete application. In it, you'll learn how to build websites and APIs, implement caching, authentication, validation, error handling, and a lot more. You'll also explore vital techniques for production applications, such as testing, monitoring, error handling, deployment, and documentation.

The first chapter is available for free, and early access supporters can get chapters two and three as well.

###FullStack 2015

[FullStack 2015](https://skillsmatter.com/conferences/6612-fullstack) is an event that's all about JavaScript, Node, and the Internet of Things, that will be held in London on 25th to 27th June.  Tickets start at &pound;375 for early bird tickets.

There's currently a [FullStack call for papers](https://docs.google.com/forms/d/1YG33cmiKHiUimB0Z6p-5BLWghZ5TsgXUM0MtKWqNbGE/viewform?c=0&w=1), so if you're interested in speaking at the conference you've got a week to apply.
