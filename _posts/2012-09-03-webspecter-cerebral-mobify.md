---
layout: post
title: "WebSpecter, cerebral.js, Mobify.js"
author: "Alex Young"
categories: 
- testing
- frameworks
- libraries
- backbone.js
- mobile
---

###WebSpecter

[WebSpecter](https://github.com/jgonera/webspecter) (License: _MIT_) by Juliusz Gonera is an acceptance test framework built using PhantomJS.  The author's examples are written with CoffeeScript, but it can be used with JavaScript as well.

The tests use a BDD-style syntax, based around "features" and CSS selectors:

{% highlight coffeescript %}
feature "GitHub search", (context, browser, $) ->
  before (done) -> browser.visit 'https://github.com/search', done

  it "finds WebSpecter", (done) ->
    $('input[name=q]').fill 'webspecter'
    $(button: 'Search').click ->
      $(link: "jgonera / webspecter").present.should.be.true
      done()

  it "looks only for users when asked to", (done) ->
    $('input[name=q]').fill 'webspecter'
    $(field: 'Search for').select 'Users'
    $(button: 'Search').click ->
      $(link: "jgonera / webspecter").present.should.be.false
      done()
{% endhighlight %}

The `browser` object is a wrapper around Phantom's `WebPage`.  A `$` function is also present which is jQuery-like but not implemented using jQuery.

###cerebral.js

[cerebral.js](http://gorillatron.github.com/cerebral/) (GitHub: [gorillatron / cerebral](https://github.com/gorillatron/cerebral)) by Andre Tangen extends Backbone.js to provide a module system and a publish/subscribe application core.  It uses RequireJS for modules and module loading, and modules are restricted to a "sandbox" designed to limit the elements the module has access to.

The main motivation behind cerebral.js is to encourage loosely coupled applications.  When I'm working on my own Backbone.js applications I usually adopt a similar approach, so it's reassuring to see the same ideas in a framework.

###Mobify.js

[Mobify.js](http://www.mobify.com/mobifyjs/) (GitHub: [mobify / mobifyjs](https://github.com/mobify/mobifyjs), License: _MIT_, npm: [mobify-client](https://npmjs.org/package/mobify-client)) is a new client-side web framework that aims to make it easier to adapt sites to any device.  This includes [responsive design](http://www.mobify.com/mobifyjs/docs/responsive/) techniques, but it can also be backed by a cloud service called [Mobify Cloud](https://cloud.mobify.com/) that includes automatic [image resizing](http://www.mobify.com/mobifyjs/docs/image-resizing/), JavaScript concatenation, and a CDN.  Mobify.js projects are built with Zepto and Dust.js.

The Mobify.js authors have also been building MIT-licensed [Mobify.js modules](http://www.mobify.com/mobifyjs/modules/), at the moment there's a carousel and an accordion.
