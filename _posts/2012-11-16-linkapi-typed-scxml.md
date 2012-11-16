---
layout: post
title: "LinkAP, typed, SCXML Simulation"
author: Alex Young
categories: 
- libraries
- testing
- node
- browser
---

###LinkAP

[LinkAP](http://linkapjs.com/) (GitHub: [pfraze / link-ap](https://github.com/pfraze/link-ap), License: _MIT_) by Paul Frazee is a client-side application platform based around web workers and services.  It actually prevents the use of what the author considers dangerous APIs, including `XMLHttpRequest` -- one of the [LinkAP design goals](https://github.com/pfraze/link-ap/wiki/Design-Document) is to create an architecture for safely coordinating untrusted programs within an HTML document.  The design document also addresses sessions:

> In LinkAP, sessions are automatically created on the first request from an agent program to a domain. Each session must be approved by the environment. If a destination responds with a 401 WWW-Authenticate, the environment must decide whether to provide the needed credentials for a subsequent request attempt.

To build a project with LinkAP, check out the [LinkAP repository](https://github.com/pfraze/link-ap) and then run `make`.  This will create a fresh project to work with.  It expects to be hosted by a web server, you can't just open the `index.html` page locally.  It comes with Bootstrap, so you get some fairly clean CSS to work with out of the box.

###typed

[typed](http://alexlawrence.github.com/typed/) (GitHub: [alexlawrence / typed](https://github.com/alexlawrence/typed), License: _MIT_, npm: [typed](https://npmjs.org/package/typed)) by Alex Lawrence is a static typing library.  It can be used with Node and browsers.  The project's homepage has live examples that can be experimented with.

A function is provided called `typed` which can be used to create constructors that bestow runtime static type checking on both native types and prototype classes.  There are two ways to declare types: comment parsing and suffix parsing:

{% highlight javascript %}
// The 'greeting' argument must be a string
var Greeter = typed(function(greeting /*:String*/) {
  this.greeting = greeting;
});

// This version uses suffix parsing
var Greeter = typed(function(greeting_String) {
  this.greeting = greeting_String;
});
{% endhighlight %}

The library can be turned off if desired by using `typed.active = false` -- this could be useful for turning it off in production environments.

The author has included a build script and tests.

###SCXML Simulation

"Check out this cool thing I built using d3: [http://goo.gl/wG5cq](http://goo.gl/wG5cq)," says Jacob Beard.  That does look cool, but what is it?  It's a visual representation of a state chart, based on [SCXML](http://en.wikipedia.org/wiki/SCXML).  Jacob has written two libraries for working with SCXML:

* A d3-based library for visualizing SCXML with SVG: [jbeard4 / scxml-viz](https://github.com/jbeard4/scxml-viz)
* An implementation of the W3C SCXML draft specification in JavaScript [jbeard4 / SCION](https://github.com/jbeard4/SCION)

We previously wrote about the SCION project in [Physijs, SCION, mmd, Sorting](http://dailyjs.com/2012/06/08/physijs-scion-mmd-sorting/).
