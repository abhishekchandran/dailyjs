---
layout: post
title: "Bobun, Backbone Eye, Rssi"
author: "Alex Young"
categories: 
- node
- modules
- backbone
- templating
---

###Bobun

[Bobun](http://neoziro.github.io/bobun/) (GitHub: [neoziro / bobun-ui](https://github.com/neoziro/bobun-ui), License: _MIT_) by Greg Bergé is a simple UI-focused data-binding library for Backbone.js:

> Bobun provides a simple way to bind a model to a view, or a view to model, a view to a view, or even a model to a model. It adds the ability to call set, get, and validate on the view. Bobun a simple way to manage and clean subviews thanks to Backbone.babysitter.

Binding a model looks like this: `Bobun.Binding.bind(modelA, modelB, 'symetricAttribute');` -- everything is namespaced under `Bobun`.  There's also `Bobun.Binding.bindTo` for one-way bindings, and there are also some view-specific features in `Bobun.View`:

{% highlight javascript %}
Bobun.View.extend({
  events: {
    'click': 'domEventTriggerProxy'
  }
});
{% endhighlight %}

###Backbone Eye

[Backbone Eye](http://dhruvaray.github.io/spa-eye/) (GitHub: [dhruvaray / spa-eye](https://github.com/dhruvaray/spa-eye), License: _Simplified BSD_) by Dhruva Ray is a Firebug extension for debugging Backbone applications:

> Backbone Eye presents application specific models and views to introspect. Models show only application specific properties and shield away internal Backbone framework details. Search for models having certain attribute values, pin interesting models or use most-used models list to dig deeper.

The project's homepage has screenshots with examples of how it handles models, collections, and views.  It has some interesting features for visualising data flows.  For example, _interaction trails_ shows a sequence of interactions which have occurred on the selected model as a result of standard Backbone write operations.

###Rssi

Rssi (GitHub: [mvasilkov / rssi](https://github.com/mvasilkov/rssi), License: _MIT_, Bower: _rssi_) by Mark Vasilkov is a string interpolation library inspired by Ruby's syntax.

> There are many template engines in JS, many unbelievably slow, while others (like doT) are quite fast but use unsafe evaluation: try {{=document.cookie}}.
> Rssi is 10x faster than Mustache, and 25-30x faster than Underscode and Lo-Dash templates (Rssi does about 1,300,000 ops/sec on my old Mac Mini, with Mustache scoring 130,000 and Lo-Dash about 45,000).
> Rssi is also marginally slower than doT, the upside being: it's perfectly safe to use, won't access global variables, call functions etc. (in fact, you can use rssi in an untrusted environment, e.g. let users customize their profile page).

If you're looking for something secure without the more abstract features of larger templating libraries, then Rssi might be a good choice.  It has unit tests and can be installed from npm or Bower.
