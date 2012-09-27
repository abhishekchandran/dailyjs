---
layout: post
title: "RoyalSlider: Tutorial and Code Review"
author: Alex Young
categories:
- libraries
- browser
- plugins
- jquery
- sponsored-content
---

<div class="sponsored-content">
  <p><a class="label" href="/sponsored-content.html">Sponsored Content</a> This post is about a commercial product that we think will appeal to DailyJS readers.</p>
</div>

![RoyalSlider](/images/posts/royalslider.png)

There are a lot of carousel-style plugins out there, and they all have various strengths and weaknesses.  However, [RoyalSlider](http://dimsemenov.com/plugins/royal-slider/) (License: _Commercial_, CodeCanyon: [RoyalSlider](http://codecanyon.net/item/royalslider-touchenabled-jquery-image-gallery/461126), Price: $12) by Dmitry Semenov is a responsive, touch-enabled, jQuery image gallery and content slider plugin, and is one of the slickest I've seen.  The author has worked hard to ensure it's fast and efficient -- it features smart lazy loading, hardware accelerated CSS3 transitions, and a memory management algorithm that ensures only visible slides are in the DOM at any one time.

The plugin is actively maintained, and has seen over a dozen updates since its release in August 2011.  It's distributed exclusively through [CodeCanyon](http://codecanyon.net), but Dmitry's site also has [documentation](http://dimsemenov.com/plugins/royal-slider/documentation/) and [details on WordPress integration](http://dimsemenov.com/plugins/royal-slider/wordpress/).  Purchasing RoyalSlider gives access to a [set of RoyalSlider templates](http://dimsemenov.com/plugins/royal-slider/templates/) that includes several types of galleries that should slot right in to your projects.

Since the plugin was originally released it has received extremely positive feedback (which is partly why it was chosen for a _Featured Content_ post) -- Dmitry has sold over 4,500 licenses, and it's earned a 5 star rating based on 378 reviews.

###Browser Support

RoyalSlider has been tested on IE7+, iOS, Opera Mobile, Android 2.0+, Windows Phone 7+, and BlackBerry OS.

###Download and Setup

![RoyalSlider's build tool](/images/posts/royalslider-build-tool.png)

RoyalSlider can be downloaded as either a development archive (that contains the original, unminified source), or a customised build can be created using Dmitry's web-based build tool (access is granted once a license has been purchased).

To add RoyalSlider to a page, ensure you've included jQuery 1.7 or above, and then include the stylesheet and JavaScript:

{% highlight html %}
<link rel="stylesheet" href="royalslider/royalslider.css">
<script src="royalslider/jquery.royalslider.min.js"></script>
{% endhighlight %}

The plugin expects a container element with the `royalSlider` class.  Each child element will be considered a slider:

{% highlight html %}
<div class="royalSlider rsDefault">
  <!-- simple image slide -->
  <img class="rsImg" src="image.jpg" alt="image desc" />

  <!-- lazy loaded image slide -->
  <a class="rsImg" href="image.jpg">image desc</a>

  <!-- image and content -->
  <div>
    <img class="rsImg" src="image.jpg" data-rsVideo="https://vimeo.com/44878206" />
    <p>Some content after...</p>
  </div>
</div>
{% endhighlight %}

Then all you need to do is run `$.fn.royalSlider`:

{% highlight javascript %}
$(function() {
  $('.royalSlider').royalSlider();
});
{% endhighlight %}

At this point options can be provided, and believe me there are [a lot of options](http://dimsemenov.com/plugins/royal-slider/documentation/#options)!

###Examples

![RoyalSlider example](/images/posts/royalslider-template.png)

The templates distributed alongside RoyalSlider include full examples with JavaScript, CSS, and HTML.  The example above is suitable for a gallery, and it includes quite a few interesting features:

* Scrolling thumbnail navigation
* Fullscreen mode
* Automatically loads higher quality images in fullscreen mode
* Responsive images using media queries
* Keyboard arrow navigation

To set up a gallery like this, all that's required is suitable images and `$.fn.royalSlider` with the options along these lines:

{% highlight javascript %}
$('#gallery-1').royalSlider({
  fullscreen: {
    enabled: true
  , nativeFS: true
  }
, controlNavigation: 'thumbnails'
, autoScaleSlider: true
, autoScaleSliderWidth: 960
, autoScaleSliderHeight: 850
, loop: false
, numImagesToPreload: 4
, arrowsNavAutoHide: true
, arrowsNavHideOnTouch: true
, keyboardNavEnabled: true
});
{% endhighlight %}

The option names are fairly verbose so it's easy to tell what they do, but I'll go over the main ones below.

* `autoScaleSlider`: This automatically updates the slider height based on the width, most of the examples use this option
* `numImagesToPreload`: Sets the number of images to load relative to the current image
* `arrowsNavAutoHide`: Hide the navigation arrows when the user isn't interacting with the plugin

###Mobile Support

![RoyalSlider running on Android and iOS](/images/posts/royalslider-mobile.png)

RoyalSlider includes several ways to support touchscreen devices.  Swipe gestures work as expected, and there are a couple of relevant options:

* `arrowsNavHideOnTouch`: Always hide arrows on touchscreen devices
* `sliderTouch`: Allows the slider to work using touch-based gestures

There are also events for dealing with gestures, which you can hook into like this:

{% highlight javascript %}
sliderInstance.ev.on('rsDragStart', function() {
  // mouse/touch drag start
});

sliderInstance.ev.on('rsDragRelease', function() {
  // mouse/touch drag end
});
{% endhighlight %}

I tested the plugin using several examples on iOS and Android 4.1 and was generally impressed by the performance.

###Code Review

When I look at jQuery plugins I usually run through the advice found in the [jQuery Plugin Authoring Guide](http://docs.jquery.com/Plugins/Authoring).  I'd like to only write about plugins that are well-written, and you'd be surprised how many are not, given that the jQuery team has worked hard to document exactly how to write a plugin.  With that in mind, I took a look at RoyalSlider's source to see how it stacks up.

RoyalSlider is split up into separate files using a modular approach.  That enables the build tool to only include what's necessary, so it's actually pretty trivial to make a build directly suited to a given project.  The code is also consistently formatted, so I strongly recommend downloading the development version just in case you've got questions that aren't answered by the documentation -- the code is easy enough to understand for an intermediate jQuery developer.

All of these modules and the main source file are wrapped in closures, so RoyalSlider doesn't introduce any messy globals.

Most of the plugin's code is based around a standard JavaScript constructor, which also adds to its readability.  This made me wonder if the author intends to port it to other JavaScript frameworks, because it seems like large portions of functionality are neatly encapsulated from jQuery's API.

In terms of low-level DOM coding and animation performance, it has Paul Irish and Tino Zijdel's `requestAnimationFrame` fixes, and uses CSS vendor prefixing where required.

####Namespacing

RoyalSlider adds these methods and objects to `$`:

* `$.rsProto`
* `$.rsCSS3Easing`
* `$.rsModules`
* `$.fn.royalSlider`

In general plugins should limit how many things they add to `$`, but I felt like the author has been careful here and only exposed what's necessary.

* Namespaces events and CSS classes, example: `keydown.rskb`
* Correctly tracks state using `royalSlider` `.data` attribute

####Other Notes

Most jQuery plugin authors seem to miss the section on using `$.extend` to handle options, but I was pleased to see Dmitry has done this.  The main jQuery method also returns `this`, so calls after `.royalSlider` can be chained as expected.

###Support and Community

RoyalSlider has its own [Tender-powered support site](http://help.dimsemenov.com/), and the author also talks to users through his Twitter account: [@dimsemenov](https://twitter.com/dimsemenov).
