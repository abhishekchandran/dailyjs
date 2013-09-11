---
layout: post
title: "jQuery Roundup: Mapael, Velge"
author: Alex Young
categories:
- jquery
- plugins
- widgets
- tags
- maps
---

<div class="intro">
Note: You can send your plugins and articles in for review through our <a href="/contact.html">contact form</a> or <a href="http://twitter.com/dailyjs">@dailyjs</a>.
</div>

###Mapael

![Mapael](/images/posts/mapael.png)

[Mapael](http://www.neveldo.fr/mapael/) (GitHub: [neveldo / jQuery-Mapael](https://github.com/neveldo/jQuery-Mapael), License: _MIT_) by Vincent Brouté is a Raphael-based vector map plugin:

> With Mapael you can display a map of the world with clickable countries. You can build data visualisations by setting some parameters in order to automatically set a color to each area of your map and generate the legend. Moreover, you can plot cities on a map with their latitude and longitude.

The basic API looks like this:

{% highlight javascript %}
$('.container').mapael({
  map: {
    name: 'world_countries'
  }
});
{% endhighlight %}

Vincent has some examples in the readme, for example, this [map of France on JSFiddle](http://jsfiddle.net/neveldo/tn5AF/).

###Velge

Velge (GitHub: [dscout / velge](https://github.com/dscout/velge), License: _MIT_, bower: _velge_) by Parker Selbert is a tag widget, inspired by the tagging UI found in Pivotal Tracker.

It supports sorting, validation, data normalization, pattern matching, keyboard shortcuts, and callback methods for things like tag addition and removal.

The API is based around a constructor:

{% highlight javascript %}
var velge = new Velge($('.container'), { single: true });
{% endhighlight %}

The instance will then accept callbacks like this:

{% highlight javascript %}
velge
  .onAdd(addCallback)
  .onRem(remCallback)
{% endhighlight %}

It's tested with Mocha and installable with Bower!
