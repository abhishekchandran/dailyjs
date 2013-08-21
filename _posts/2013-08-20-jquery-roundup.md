---
layout: post
title: "jQuery Roundup: Fine Uploader, SimpleSlideView, jQuery.uheprnGen"
author: Alex Young
categories:
- jquery
- plugins
- ui
- widgets
- mobile
- html5
- cryto
---

<div class="intro">
Note: You can send your plugins and articles in for review through our <a href="http://contact.dailyjs.com/project">contact form</a>.
</div>

###Fine Uploader

![Fine Uploader](/images/posts/fineuploader.png)

[Fine Uploader](http://fineuploader.com/) (GitHub: [Widen / fine-uploader](https://github.com/Widen/fine-uploader), License: _GPLv3_) by Mark Feltner is a client-side library for managing file uploads.  It's free of dependencies, but there's a jQuery plugin for convenience.  It supports multiple file uploads, progress bar, drag and drop, upload cancelation, validation, and direct to Amazon S3 uploads.  S3 uploads work using CORS, and [XHR2](http://www.w3.org/TR/XMLHttpRequest2/) is used for browsers with File API support and monitoring upload progress.

The author maintains a blog about the project, and a [recent post](http://blog.fineuploader.com/2013/08/16/fine-uploader-3-8-released/) includes details on the S3 support.

###SimpleSlideView

[SimpleSlideView](http://blog.cloudfour.com/simpleslideview/) (GitHub: [cloudfour / SimpleSlideView](https://github.com/cloudfour/SimpleSlideView), License: _MIT_) by Tyler Sticka is a mobile-style UI widget for displaying and managing animated view hierarchies:

> This plugin was designed to work well with non-fixed layouts, which means it can be helpful to scroll to the top of the window or container prior to a view changing. If a `$.scrollTo` plugin is available, SimpleSlideView will attempt to use it by default. It has been tested with jquery.scrollTo and ZeptoScroll.

The views are divs marked up with a container so they can be displayed and hidden as needed.  Data attributes are used to associate navigation with markup: a link with `data-popview` or `data-pushview` allows movement through the view hierarchy.  There's also a JavaScript API for managing this.

The readme has full documentation and an example for using it in a responsive interface.

###jQuery.uheprnGen

[jQuery.uheprnGen](http://ryanmcdonough.co.uk/prng/index.html) (GitHub: [ryanmcdonough / jQuery.uheprnGen](https://github.com/ryanmcdonough/jQuery.uheprnGen), License: _Public Domain_) is Ryan McDonough's first attempt at a jQuery plugin, but it's cool because it wraps around [Steve Gibson's UHE PRNG script](https://www.grc.com/otg/uheprng.htm), which stands for _Ultra-High Entropy Pseudo-Random Number Generator_.

> This carefully designed PRNG utilizes more than 1536 bits of internal state memory. The operating parameters of the generator's algorithm were carefully chosen (it uses a safe prime factor) to guarantee that every possible PRNG state is visited before the sequence begins to repeat.

With Ryan's script, you can call `$(this).uheprngGen({ range: 100, count: 10001 });` to generate 10001 random numbers with a range of 0 to 100.

