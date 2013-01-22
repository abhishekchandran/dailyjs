---
layout: post
title: "jQuery Roundup: Plugin Registry, imagemax, jQuery Sortable"
author: Alex Young
categories:
- jquery
- plugins
- sortable
- galleries
- slideshow
---

<div class="intro">
Note: You can send your plugins and articles in for review through our <a href="/contact.html">contact form</a> or <a href="http://twitter.com/dailyjs">@dailyjs</a>.
</div>

###jQuery Plugin Registry

<div class="image">
  <img src="/images/posts/jquery-plugin-registry.png" alt="" />
  <small>jQuery: Write once, do more, then write a weird framework-specific manifest file, learn Git, then share!</small>
</div>

The new [jQuery Plugin Registry](http://plugins.jquery.com/) has finally been released.  It's based on WordPress, and you can download the source from GitHub: [plugins.jquery.com](https://github.com/jquery/plugins.jquery.com).

To list a plugin on the registry, take a look at the [Publishing Your Plugin](http://plugins.jquery.com/docs/publish/) guide.  The workflow is based around Git, and you'll need to write a `jquery.json` manifest file so the registry can display appropriate metadata.  Even though dependencies are listed, there isn't an official automated tool for installing them (a jQuery npm or component equivalent):

> If you're looking to just browse and use jQuery plugins in your application or site, not a lot has changed. Plugins each have basic pages that provide a link to the plugin download, as well as past versions, documentation, issue tracker, and source code repository. Download links may serve you a zip file with the plugin assets, or link to the best resource to download the build of the plugin you're looking for.

Given the amount of people writing JavaScript libraries with an _optional_ jQuery support layer, having to add an extra file just to get published on a website seems odd to me.  While it means you don't need to create an account on the plugin registry site, people will end up with several json files littering their repositories and getting out of sync.  There's probably already a Node tool for automatically generating jQuery, Component/Bower, and npm/Ender json files.

###imagemax

[imagemax](http://zerostatic.com/imagemax/) (GitHub: [zerostatic / imagemax](https://github.com/zerostatic/imagemax), License: _MIT_) by Matt Wallace is a fullscreen slideshow plugin.  Images are displayed in the background and scaled to fit the window.

Like other gallery plugins, this one will display a set of images in a container, but it also takes an array of images as an argument:

{% highlight javascript %}
$('#bg').imagemax({
  imageArray: ['img/bg1.jpg','img/bg2.jpg','img/bg3.jpg']
, autoPlay: 4000
});
{% endhighlight %}

###jQuery Sortable

[jQuery Sortable](http://johnny.github.com/jquery-sortable/) (GitHub: [johnny / jquery-sortable](https://github.com/johnny/jquery-sortable), License: _BSD3_) by Jonas von Andrian is a drag-and-drop sort library that doesn't require jQuery UI.  It supports nested lists, and the demo (with default options) shows a nice "drop" indicator so it's easy to see where an element is being moved to.

The author has demonstrated it being used with Bootstrap, and it works well with Bootstrap's markup and styles.  It allows tables to be sorted, but this won't work as well in Konqueror or IE.

