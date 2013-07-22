---
layout: post
title: "Feaxures, RBush, Bootstrap Modal"
author: Alex Young
categories: 
- libraries
- modules
- bootstrap
- node
- ui
---

###Feaxures

![Feaxures](/images/posts/feaxures.png)

[Feaxures](http://www.feaxures.com/) (GitHub: [adrianmiu / feaxures](https://github.com/adrianmiu/feaxures), License: _MIT_) by Adrian Miu is a progressive enhancement library that combines ideas from the DRY principle, responsive design, A/B testing, and RequireJS:

> RequireJS is used to handle the process of loading asyncronously the JS/CSS files. It also helps with managing the depencies. For example if the `jquery.ui.tabs.js` file is dependent on `jquery.ui.widget.js` file, RequireJS will load that file first, assuming you have configured it properly using the `shim` option.

Once you've configured your RequireJS loader script, data attributes prefixed with `data-fxr-` are used to tie specific features to blocks of markup.  The attribute's value can be set to several things including URL query strings, JSON, and DOM IDs to pass options to the feature.

The Feaxures API also has lifecycle events so you can see when features are loaded and attached.

###RBush

RBush (GitHub: [mourner / rbush](https://github.com/mourner/rbush), License: _MIT_, npm: [rbush](https://npmjs.org/package/rbush)) by Vladimir Agafonkin is a high-performance 2D spatial indexer for points in rectangles:

> Spatial index is a special data structure for points and rectangles that allows you to perform queries like "all items within this bounding box" very efficiently (e.g. hundreds of times faster than looping over all items). It's most commonly used in maps and data visualizations.

Trees can be created and values subsequently inserted like this:

{% highlight javascript %}
var tree = rbush(9, ['.minLng', '.minLat', '.maxLng', '.maxLat']);
tree.insert({id: 'foo', minLng: 30, minLat: 50, maxLng: 40, maxLat: 60});
{% endhighlight %}

Data can also be inserted in bulk by using arrays, and values can be searched, removed, and exported.  It also works in browsers.  The readme has some interesting papers related to r-trees, and Vladimir has included unit tests written with Mocha.

###Bootstrap Modal

Bootstrap Modal (GitHub: [cabaret / bootstrap-modal-strict-close](https://github.com/cabaret/bootstrap-modal-strict-close), License: _Apache 2.0_) by Joris Ooms is a small extension to Bootstrap's modal dialog to prevent it from being accidentally closed when triggering actions like form submission.

Use it by adding the attribute `data-strict-close="true"` or passing `strictClose: true` to the `.modal` method's options.
