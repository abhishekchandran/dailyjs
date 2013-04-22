---
layout: post
title: "Object.observe Shim, Behave, Snap.js"
author: Alex Young
categories:
- shims
- textarea
- mobile
- ui
---

###Object.observe Shim

It's encouraging to see Harmony taking on board influences from databinding frameworks, given how important they're proving to be to front-end development.  The proposed [Object.observer API](http://wiki.ecmascript.org/doku.php?id=harmony:observe) aims to improve the way respond to changes in objects:

> Today, JavaScript framework which provide databinding typically create objects wrapping the real data, or require objects being databound to be modified to buy in to databinding. The first case leads to increased working set and more complex user model, and the second leads to siloing of databinding frameworks.  A solution to this is to provide a runtime capability to observe changes to an object

François de Campredon sent in KapIT's [Object.observe shim](https://github.com/KapIT/observe-shim/) (GitHub: [KapIT / observe-shim](https://github.com/KapIT/observe-shim/), License: _Apache_), which implements the algorithm described by the proposal.  It's compatible with ECMAScript 5 browsers, and depends on a method called `ObserveUtils.defineObservableProperties` for setting up the properties you're interested in observing.  The readme has more documentation and build instructions.

###Behave.js

[Behave.js](http://jakiestfu.github.io/Behave.js/) (GitHub: [jakiestfu / Behave.js](https://github.com/jakiestfu/Behave.js), License: _MIT_) by Jacob Kelley is library for adding IDE-like behaviour to a `textarea`.  It doesn't have any dependencies, and has impressive browser support.  Key features include hard and soft tabs, bracket insertion, and automatic and multiline indentation.

Basic usage is simply:

{% highlight javascript %}
var editor = new Behave({
  textarea: document.getElementById('myTextarea')
});
{% endhighlight %}

There is also a function for binding events to Behave -- the events are all documented in the readme, and include things like key presses and lifecycle events.

###Snap.js

[Snap.js](http://jakiestfu.github.io/Snap.js/demo/apps/default.html) (GitHub: [jakiestfu / Snap.js](https://github.com/jakiestfu/Snap.js/), License: _MIT_) also by Jacob is another dependency-free UI component.  This one is for creating mobile-style navigation menus that appear when clicking a button or dragging the entire view.  It uses CSS3 transitions, and has an event-based API so it's easy to hook it into existing interfaces.

The drag events use 'slide intent', which allows an integer to be specified (`slideIntent`) to control the angle at which a gesture is considered horizontal.  Jacob has included helpful documentation on how to structure and style a suitable layout for the plugin:

> Two absolute elements, one to represent all the content, and another to represent all the drawers. The content has a higher z-index than the drawers. Within the drawers element, it's direct children should represent the containers for the drawers, these should be fixed or absolute.

He has lots of other useful client-side projects on [GitHub/jakiestfu](https://github.com/jakiestfu?tab=repositories).
