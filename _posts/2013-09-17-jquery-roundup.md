---
layout: post
title: "jQuery Roundup: persistState, CLNDR.js"
author: Alex Young
categories:
- jquery
- plugins
- widgets
- calendars
- time
- forms
---

<div class="intro">
Note: You can send your plugins and articles in for review through our <a href="/contact.html">contact form</a> or <a href="http://twitter.com/dailyjs">@dailyjs</a>.
</div>

###persistState

[persistState](http://togakangaroo.github.io/persistState/) (GitHub: [togakangaroo / persistState](https://github.com/togakangaroo/persistState), License: _MIT_) by George Mauer saves the state of UI widgets.  It can be applied to a selector, so you can save the state of a specific set of widgets rather than all of them.

I like the idea of using this to save the state of form controls, particularly in a multi-stage form that's handled client-side.  Values are saved to `localStorage`, and the API of `persistState` allows you to swap in your own serialisation handler.

Saving the state of form controls looks like this:

{% highlight javascript %}
$.ow.persistState.elementPersistence['textarea,input:not(:checkbox),select'] = {
  saveState: function($el) {
    return { val: $el.val() };
  },

  restoreState: function($el, state) {
    if (!state) return;
    if ($el.val() !== state.val)
      $el.val(state.val).trigger('change');
  }
};
{% endhighlight %}

###CLNDR.js

[CLNDR.js](http://kylestetz.github.io/CLNDR/) (GitHub: [kylestetz / CLNDR](https://github.com/kylestetz/CLNDR), License: _MIT_) by Kyle Stetz is a calendar plugin:

> There are wonderful and feature-rich calendar modules out there and they all suffer the same problem: they give you markup (and often a good heap of JS) that you have to work with and style. This leads to a lot of hacking, pushing, pulling, and annoying why-can't-it-do-what-I-want scenarios.

> CLNDR doesn't generate markup (well, it has some reasonable defaults, but that's an aside). Instead, CLNDR asks you to create a template and in return it supplies your template with a great set of objects that will get you up and running in a few lines.

CLNDR requires Moment.js, which is OK because I don't leave home without it!
