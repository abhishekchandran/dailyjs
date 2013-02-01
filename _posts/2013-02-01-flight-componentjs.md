---
layout: post
title: "Flight, ComponentJS"
author: "Alex Young"
categories: 
- components
- twitter
---

###Flight

![Flight by Twitter](/images/posts/flight.png)

What's the most sensible thing to do when there's an established project called [Component](https://github.com/component/component) that aims to make client-side development more modular through reusable components?  Invent something else that yet again overloads this increasingly overused term!  If you weren't already [confused about components](http://dailyjs.com/2013/01/28/components/), then get ready to unlearn everything you've learned.

I was expecting this, however.  After seeing Bower, I felt like it really needed another project to further abstract client-side development, and that appears to have been satisfied by the release of Flight.

[Flight](http://twitter.github.com/flight/) (GitHub: [twitter / flight](https://github.com/twitter/flight), License: _MIT_, bower: _flight_) from Twitter is a new framework that maps "behaviour" to DOM nodes.  To do this it brings together a few things you're probably already familiar with: multiple inheritance (mixins), the AMD pattern, and the observer pattern.  The supplied [Flight Mail](http://twitter.github.com/flight/demo/) example app is built using RequireJS, so you can see why AMD is relevant here.

Flight apps look a bit like Backbone/RequireJS apps.  They both use AMD and rely on events for communication.  However, Flight is deceptively different.  Which isn't necessarily a bad thing, because we've argued about MVC/MVVC/MV* for a long time at this point.

The authors define a component in Flight as a constructor with properties mixed in.  Each component has event handling, and is eventually attached to a DOM node.  They can't refer to each other directly -- communication is purely through events.

That last point is potentially important, because it demonstrates the authors have a good sense of one of the major issues with client-side development: writing reusable, decoupled code.  Given that Angus Croll and Dan Webb are contributors to this project, it's not surprising that there's a focus on composition.

Although Flight already has a bazillion stars on GitHub (Twitter&trade;!), it's going to face the same hurdles in adoption as Backbone did: the learning curve.  Casual JavaScript developers are going to see AMD, mixin, and "advice", and struggle to understand how to relate these concepts to their existing development practices.

However, the project has some great ideas and has serious pedigree behind it.  It's different enough to Backbone, AngularJS, and Knockout, so I've welcomed it to my rapidly growing client-side development toy box.

###ComponentJS

[ComponentJS](http://componentjs.com/) (GitHub: [rse / componentjs](https://github.com/rse/componentjs), License: _MPL_) by Ralf S. Engelschall is a totally unrelated project that just happens to involve the term "component".  This library is aimed at creating dialog-based hierarchical interfaces for single page apps.  It has an OO library, a graphical debugger, UI toolkit, state transitions, and communication using events.

According to the author, this project has been developed since 2009 (although the domain name was created a year ago), so the naming clash is purely coincidental from what I can tell.  It has extremely detailed API documentation, and a [demo with browsable source code](http://componentjs.com/demo.html).

