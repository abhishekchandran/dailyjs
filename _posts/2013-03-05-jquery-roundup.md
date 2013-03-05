---
layout: post
title: "jQuery Roundup: 2.0 Beta 2, Alpha Image, jqTree"
author: Alex Young
categories:
- jquery
- plugins
- tree
- widgets
- images
- Canvas
---

<div class="intro">
Note: You can send your plugins and articles in for review through our <a href="/contact.html">contact form</a>.
</div>

###jQuery 2.0 Beta 2

[jQuery 2.0 Beta 2](http://blog.jquery.com/2013/03/01/jquery-2-0-beta-2-released/) is out, which has fixes for most of the major parts of the framework.  This version also includes a Grunt build script, so you can build custom versions of jQuery more easily.  The announcement posts suggests swapping out Sizzle for another selector engine.

jQuery 2.0 removes compatibility for IE before version 9, so you'll have to use 1.9 if you want to support legacy browsers.

###jQuery Alpha Image

[jQuery Alpha Image](http://sly777.github.com/Jquery-Alpha-Image/) (GitHub: [Sly777 / Jquery-Alpha-Image](https://github.com/Sly777/Jquery-Alpha-Image), License: _MIT/GPL_, bower: _Jquery-Alpha-Image_) by İlker Güller uses a temporary Canvas to make a colour in an image transparent.  It supports RGB and hex colours and has a callback that runs when the process has finished:

{% highlight javascript %}
$('.example3').alphaimage({
  colour: '#9CDAF0',
  onlyData: true,
  onComplete: function(result) {
    console.log(result);
  }
});
{% endhighlight %}

###jqTree

[jqTree](http://mbraak.github.com/jqTree/) (GitHub: [mbraak / jqTree](https://github.com/mbraak/jqTree), License: _Apache 2.0_) by Marco Braak is a widget that creates trees using unordered lists based on JSON data.  It supports drag and drop for reordering items or moving them between parents, and supports IE7+.

The author has included tests, and the documentation is detailed, with lots of examples.  The events API is thoughtful as well -- you can even track when items are added to the tree with `onCreateLi`:

{% highlight javascript %}
$('#tree1').tree({
  data: data,
  onCreateLi: function(node, $li) {
    // Add 'icon' span before title
    $li.find('.jqtree-title').before('<span class="icon"></span>');
  }
});
{% endhighlight %}

