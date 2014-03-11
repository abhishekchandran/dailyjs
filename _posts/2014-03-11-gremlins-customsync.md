---
layout: post
title: "Gremlins.js, Backbone.CustomSync"
author: Alex Young
categories:
- testing
- backbone
---

###Gremlins.js

![Gremlins.js](/images/posts/monkeytesting.gif)

Gremlins.js (GitHub: [marmelab / gremlins.js](https://github.com/marmelab/gremlins.js), License: _MIT_) from marmelab is a monkey testing library.  According to the authors, it can be used to unleash a horde of undisciplined gremlins at a web application.

If that sounds weird, there's a handy gif in the readme that illustrates how it works: it basically throws events at your HTML, and is able to report back when something goes wrong:

> Mogwais only monitor the activity of the application and record it on the logger. For instance, the "fps" mogwai monitors the number of frame per second, every 500ms.
> Mogwais also report when gremlins break the application. For instance, if the number of frames per seconds drops below 10, the fps mogwai will log an error.

There are various kinds of gremlins that try to uncover issues.  This includes a form filler, clicker, and scroller.  You can manually create hordes using a chainable API:

{% highlight javascript %}
gremlins.createHorde()
  .gremlin(gremlins.species.formFiller())
  .gremlin(gremlins.species.clicker().clickTypes(['click']))
  .gremlin(gremlins.species.scroller())
  .gremlin(function() {
    window.$ = function() {};
  })
  .unleash();
{% endhighlight %}

###Backbone.CustomSync

Garrett Murphey sent in [Backbone.CustomSync](http://gmurphey.com/2014/03/09/backbone-custom-sync.html#.Ux9J7ud_tbU) (GitHub: [gmurphey / backbone.customsync](https://github.com/gmurphey/backbone.customsync), License: _MIT_, npm: [backbone.customsync](https://www.npmjs.org/package/backbone.customsync)), a more pragmatic solution for defining `Backbone.sync` implementations that allows you to avoid giant `switch` statements:

> To use the extension, all you have to do is use `Backbone.CustomSync.Model` or `Backbone.CustomSync.Collection` in place of `Backbone.Model` and `Backbone.Collection`, respectively.
> If you don't define one of these sync methods - `createSync`, for example - and Backbone attempts to save a new model, the `options.error` callback will be invoked automatically. Backbone.CustomSync will only perform the operations you define.


