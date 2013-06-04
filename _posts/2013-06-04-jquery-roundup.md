---
layout: post
title: "jQuery Roundup: 1.10.1, 2.0.2, ikSelect, photoWall.js"
author: Alex Young
categories:
- jquery
- plugins
- select
- galleries
- images
---

<div class="intro">
Note: You can send your plugins and articles in for review through our <a href="/contact.html">contact form</a>.
</div>

###jQuery 1.10.1 and 2.0.2

"A new release already? It's only been a week! Yes, because you deserve it.  We're greatly encouraged by all the people who upgraded and found our well-hidden 'we completely hosed relative animations' easter egg," writes Dave Methvin, about the release of [jQuery 1.10.1 and 2.0.2](http://blog.jquery.com/2013/05/30/jquery-1-10-1-and-2-0-2-released/).

The full background to this bug was documented in [ticket #13939](http://bugs.jquery.com/ticket/13939).  Another [animation-related bug was fixed](http://bugs.jquery.com/ticket/13937), and an [IE selector/iframe issue](http://bugs.jquery.com/ticket/13936) as well.

###ikSelect

[ikSelect](http://igor10k.github.io/ikSelect/) (GitHub: [Igor10k / ikSelect](https://github.com/Igor10k/ikSelect)) by "Igor10k" is another `select` replacement plugin!  This one supports custom markup and `inline-block`, `optgroup`, adding and removing `option`s, callbacks, and event triggers.

The API is clean and idiomatic jQuery.  There's a single entry point, `$(selector).ikSelect` which can be used to apply the plugin to a `select`, or issue commands to an instance of ikSelect.  Various options are supported, like setting the width automatically and adding search support (known as filtering in this case).

###photoWall.js

[photoWall.js](http://jeremyjcpaul.com/photo-wall-demo.php) (GitHub: [jeremyjcpaul / photowall](https://github.com/jeremyjcpaul/photowall), License: _MIT_, jQuery: [photowall](http://plugins.jquery.com/photowall/)) by Jeremy JC Paul creates a photo gallery in a similar style to Google+/Picasa, where clicking on an image opens a panel that displays additional metadata.

The markup allows the photo's title and description to be specified like this:

{% highlight javascript %}
<div class="photowall">
  <div class="pw-slide">
    <img class="pw-image" src="images/image-filename.jpg" />
    <div class="pw-image-desc">
      <!-- Any HTML content can go in here. -->
    </div>
  </div>
</div>
{% endhighlight %}

The plugin is invoked using `$(selector).photoWall()`, and supported options include event handlers and animation speed.
