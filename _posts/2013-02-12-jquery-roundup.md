---
layout: post
title: "jQuery Roundup: Formwin, Three Sixty Slider, slideToucher"
author: Alex Young
categories:
- jquery
- plugins
- animations
- forms
- ui
---

<div class="intro">
Note: You can send your plugins and articles in for review through our <a href="/contact.html">contact form</a>.
</div>

###Formwin

[Formwin](http://rocco.github.com/formwin/) (GitHub: [rocco / formwin](https://github.com/rocco/formwin), License: _MIT_) by Rocco Georgi started as a fork of [Uniform](https://github.com/pixelmatrix/uniform), but is now very different.  It removes legacy browser support (IE8+) and relies on CSS for things like rounded corners.

The required markup is documented in the project's readme.  In general it relies on labels and spans:

{% highlight html %}
<label class="formwintexts">
  <span>Label Text</span>
  <input type="text" name="yourinput">
</label>
{% endhighlight %}

It must be initialised to be used on a page, either with `$.formwin.init();` or by setting `$.formwinSettings`.  The `init` method accepts several options for configuring which CSS classes get used for things like active elements and hovering.  This is similar to Uniform, and makes it extremely easy to drop into an existing project.

###Three Sixty Slider

![360](/images/posts/360jquery.png)

[Three Sixty Slider](http://creativeaura.github.com/threesixty-slider/) (GitHub: [creativeaura / threesixty-slider](https://github.com/creativeaura/threesixty-slider), License: _MIT/GPL_) by Gaurav Jassal allows multiple images to be displayed to give the illusion of multiple viewing angles.  It features smooth animations, mouse and touchscreen support, and has a lot of tweakable options.

Basic usage is like this:

{% highlight javascript %}
$('.product1').ThreeSixty({
  totalFrames: 72, // Total no. of image you have for 360 slider
  endFrame: 72, // end frame for the auto spin animation
  currentFrame: 1, // This the start frame for auto spin
  imgList: '.threesixty_images', // selector for image list
  progress: '.spinner', // selector to show the loading progress
  imagePath:'/assets/product1/', // path of the image assets
  filePrefix: 'ipod-', // file prefix if any
  ext: '.jpg', // extension for the assets
  height: 265,
  width: 400,
  navigation: true
});
{% endhighlight %}

It'll figure out the image names based on the settings, so the markup doesn't need to include lots of `img` tags.  There's a live demo on [creativeaura.github.com/threesixty-slider/](http://creativeaura.github.com/threesixty-slider/).

###slideToucher

slideToucher (GitHub: [Yuripetusko / slideToucher](https://github.com/Yuripetusko/slideToucher), License: _MIT_) by Yuri Petusko is a swipe gesture plugin that is designed to be high performance.  It supports horizontal and vertical swipes, and uses `translate3d` to produce smooth animations where available.

It expects markup with the `slide` and `row` classes, and is invoked with `$(selector).slideToucher({ vertical: true, horizontal: true });`.  The author has posted a demo here: [yuripetusko.github.com/slideToucher/](http://yuripetusko.github.com/slideToucher/).
