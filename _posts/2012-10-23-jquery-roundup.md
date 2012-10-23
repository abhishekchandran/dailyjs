---
layout: post
title: "jQuery Roundup: Fuel UX, uiji.js, QuoJS"
author: Alex Young
categories:
- jquery
- jquery-ui
- bootstrap
- mobile
---

<div class="intro">
Note: You can send your plugins and articles in for review through our <a href="/contact.html">contact form</a> or <a href="http://twitter.com/dailyjs">@dailyjs</a>.
</div>

###Fuel UX

![Fuel UX](/images/posts/fuelux.png)

[Fuel UX](http://exacttarget.github.com/fuelux) (GitHub: [ExactTarget / fuelux](https://github.com/ExactTarget/fuelux), License: _MIT_) from ExactTarget is a lightweight library that extends Twitter Bootstrap with some additional JavaScript controls, a Grunt build, and AMD compatibility.  At launch, the following controls are included:

* Combobox - _combines input and dropdown for easy and flexible data selection_
* Datagrid - _renders data in a table with paging, sorting, and searching_
* Pillbox - _manages selected items with color-coded text labels_
* Search - _combines input and button for integrated search interaction_
* Spinner - _provides convenient numeric input with increment and decrement buttons_

The project is well-documented, covered in unit tests, and outside contributions are welcome and encouraged.

_Contributed by Adam Alexander_

###uiji.js

![uiji.js](/images/posts/uijijs.png)

[uiji.js](http://aakilfernandes.com/uiji.html) (GitHub: [aakilfernandes / uiji](https://github.com/aakilfernandes/uiji)) by Aakil Fernandes is a clever hack that inverts jQuery by allowing CSS selectors to create elements.  This will create a paragraph with the class `greeting`, that contains the text `Hello World!`:

{% highlight javascript %}
$('#helloWorld .output').uiji('p.greeting"Hello World!"')
{% endhighlight %}

Callbacks can be used to create hierarchy, and the API is chainable because the plugin returns `$(this)` once it has processed the input.

###QuoJS

[QuoJS](http://quojs.tapquo.com/) (GitHub: [soyjavi / QuoJS](https://github.com/soyjavi/quojs), License: _MIT_) by Javier Jiménez is a small library for mobile development.  It supports HTML traversal and abstractions for touch-based gestures.  It doesn't require jQuery, but has a similar API:

{% highlight javascript %}
// Subscribe to a tap event with a callback
$$('p').tap(function() {
  // Affects "span" children/grandchildren
  $$('span', this).style('color', 'red');
});
{% endhighlight %}

The same author has written a few other ambitious projects, including [Monocle](http://monocle.tapquo.com/) (GitHub: [soyjavi / monocle](https://github.com/soyjavi/monocle), License: _MIT_), which is an MVC framework for CoffeeScript application development.

