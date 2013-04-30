---
layout: post
title: "jQuery Roundup: Sco.js, Datepicker Skins, LocationHandler"
author: Alex Young
categories:
- jquery
- plugins
- jquery-ui
- datepicker
- bootstrap
- history
---

<div class="intro">
Note: You can send your plugins and articles in for review through our <a href="/contact.html">contact form</a>.
</div>

###Sco.js

[Sco.js](http://terebentina.github.io/sco.js/) (GitHub: [terebentina / sco.js](https://github.com/terebentina/sco.js), License: _Apache 2.0_) by Dan Caragea is a collection of Bootstrap components.  They can be dropped into an existing Bootstrap project, or used separately as well.

Some of the plugins are replacements of the Bootstrap equivalents, but prefixed with `$.scojs_`.  There are also a few plugins that are unique to Sco.js, like `$.scojs_valid` for validating forms, and `$.scojs_countdown` for displaying a stopwatch-style timer.

In cases where Sco.js replaces Bootstrap plugins, the author has been motivated by simplifying the underlying markup and reducing the reliance on IDs.

Dan has included tests, and full documentation for each plugin.

###jQuery Datepicker Skins

![jQuery datepicker skins](/images/posts/jquery-datepicker-skins.png)

Artan Sinani sent in these [jQuery datepicker skins](http://rtsinani.github.io/jquery-datepicker-skins/) (GitHub: [rtsinani / jquery-datepicker-skins](https://github.com/rtsinani/jquery-datepicker-skins)).  They're tested with jQuery UI v1.10.1 and jQuery 1.9.1, so they should work with new projects quite nicely.

###LocationHandler

LocationHandler (GitHub: [slv / LocationHandler](https://github.com/slv/LocationHandler)) by Michele Salvini is a plugin for managing pushState and onpopstate.  It emits events for various stages of the history change life cycle.  Each supported state is documented in the readme, but the basic usage looks like this:

{% highlight javascript %}
$(document).ready(function() {
  var locationHandler = new LocationHandler({
    locationWillChange: function(change) {
    },
    locationDidChange: function(change) {
    }
  });
});
{% endhighlight %}

The `change` object has properties for the from/to URLs, and page titles as well.

