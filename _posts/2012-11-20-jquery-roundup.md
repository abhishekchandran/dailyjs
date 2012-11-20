---
layout: post
title: "jQuery Roundup: pickadate.js, jQuery Interdependencies, Timer.js"
author: Alex Young
categories:
- jquery
- date-pickers
- forms
- timers
---

<div class="intro">
Note: You can send your plugins and articles in for review through our <a href="/contact.html">contact form</a> or <a href="http://twitter.com/dailyjs">@dailyjs</a>.
</div>

###pickadate.js

![pickadate.js](/images/posts/pickadate.png)

[pickadate.js](http://amsul.github.com/pickadate.js/) (GitHub: [amsul / pickadate.js](https://github.com/amsul/pickadate.js), License: _MIT_) by Amsul is a date picker that works with `type="date"` or regular text fields, supports various types of date formatting options, and is easy to theme.

The [pickadate.js](http://amsul.github.com/pickadate.js/docs.htm) documentation explains how to use and configure the plugin.  Basic usage is just `$('.datepicker').datepicker()`, given a suitable form field.

###jQuery Interdependencies

[jQuery Interdependencies](http://miohtama.github.com/jquery-interdependencies/docs/) (GitHub: [miohtama / jquery-interdependencies](https://github.com/miohtama/jquery-interdependencies), License: _MIT_) by Mikko Ohtamaa is a plugin for expressing relationships between form fields.  Rule sets can be created that relate the value of a field to the presence of another field.  The simplest example of this would be selecting "Other", and then filling out a value in a text field.

It works with all standard HTML inputs, and can handle nested decision trees.  There's also some detailed documentation, [jQuery Interdependencies documentation](http://miohtama.github.com/jquery-interdependencies/docs/#!/api) and an [introductory blog post](http://opensourcehacker.com/2012/11/19/create-complex-form-field-showing-and-hiding-rules-with-jquery-interdependencies-library/) that covers the basics.

###Timer.js

Florian Schäfer sent in his forked version of jQuery Chrono, [Timer.js](https://github.com/fschaefer/Timer.js).  It's a periodic timer API for browsers and Node, with some convenience methods and time string expression parsing:

{% highlight javascript %}
timer.every('2 seconds', function () {});
timer.after('5 seconds', function () {});
{% endhighlight %}

He also sent in [Lambda.js](https://github.com/fschaefer/Lambda.js) which is a spin-off from Oliver Steele's functional-javascript library.  String expressions are used to concisely represent small functions, or lambdas:

{% highlight javascript %}
lambda('x -> x + 1')(1); // => 2
lambda('x y -> x + 2*y')(1, 2); // => 5
lambda('x, y -> x + 2*y')(1, 2); // => 5
{% endhighlight %}
