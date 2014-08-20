---
layout: post
title: "DeLorean, Cash: Call, Collect, Assign"
author: "Alex Young"
categories:
- libraries
- ui
- flux
---

###DeLorean.js

DeLorean.js (GitHub: [f / delorean](https://github.com/f/delorean), License: _MIT_, Bower: _delorean_, npm: [delorean.js](https://www.npmjs.org/package/delorean.js)) by Fatih Kadir Akın is a [Flux implementation](http://facebook.github.io/react/docs/flux-overview.html).  It can be used with React.js and Flight.js, and the author mentioned that he's working on Backbone.js integration as well.

I've previously written about [Fluxxor](http://dailyjs.com/2014/05/27/flux/), which is another library based on Flux.  If you've used MVC libraries before, then you can think of DeLorean.js and Fluxxor like alternatives for the models and controllers.  Flux provides tools for creating stores, dispatchers, and action creators.

Stores are a bit like models, but you don't create instances of them.  Instead they manage state for a domain within the application.  This actually has positive implications for testing.  This quote is from the [React overview](http://facebook.github.io/react/docs/flux-overview.html):

> Stores accept updates and reconcile them as appropriate, rather than depending on something external to update its data in a consistent way. Nothing outside the store has any insight into how it manages the data for its domain, helping to keep a clear separation of concerns. This also makes stores more testable than models, especially since stores have no direct setter methods like setAsRead(), but instead have only an input point for the payload, which is delivered through the dispatcher and originates with actions.

Dispatchers manage data flows, responding to actions as they are created during the lifetime of a program.  Action creators are similar to controllers in MVC -- in DeLorean's documentation they do things like get JSON from a server, then pass the data to a dispatcher.

Action creators are then used by the view layer, so if you're using React you could invoke action creators from views and bind them to template fragments.

This might all sound highly abstract, but you might find it useful if you're finding it hard to manage large client-side projects.  The model layer in MVC libraries often feels ORM-inspired, which in my experience doesn't always work well when combined with business logic.

###Cash Updates

Rob Robbins sent in a note to say [Cash](https://github.com/sudo-js/cash) has been updated to include new methods for allowing the invocation of native functionality:

> Call, Collect and Assign
>
> In order to keep code creep at a minimum, We are introducing these three methods that allow the invocation of native functionality on the elements in the `q`. What do I mean? Let's take the Attribute methods for an example. We could write separate methods for the getting, setting, and removal of attributes:

{% highlight javascript %}
cash.setAttribute = function(foo, bar) {
  // set attribute 'foo' to 'bar' on each element in the q 
};

cash.removeAttribute = function(foo) {
  // remove attribute 'foo' from each element in the q 
};

cash.getAttribute = function(foo) {
  // collect and return attribute 'foo' from each element in the q 
};
{% endhighlight %}

> Instead we can have a single method capable invoking any of these (or any native method for that matter):

{% highlight javascript %}
$(foo).call('setAttribute', 'data-foo', 'bar'); // returns cash
$(foo).call('removeAttribute', 'data-foo');
$(foo).collect('getAttribute', 'data-foo'); // retruns an array
{% endhighlight %}

The reason I [wrote about Cash previously](http://dailyjs.com/2014/07/17/cash/) was because I know a lot of people are looking for alternatives to jQuery for smaller DOM/event-wrapper libraries, and this new API should help people use existing standards rather than reinventing things browsers are good at.
