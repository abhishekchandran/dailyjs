---
layout: post
title: "HHHHold, w2ui, Event Spy"
author: Alex Young
categories: 
- node
- testing
- ui
- events
- jquery
---

###HHHHold

HHHHold (GitHub: [ThisIsJohnBrown / hhhhold-js](https://github.com/ThisIsJohnBrown/hhhhold-js), License: _MIT_) is a library for faking user generated content with [hhhhold!](http://hhhhold.com/):

> Drop hhhhold URLs into your code for quick access to safe-for-work, attributed images from ffffound. Simulate real user content in your project.

It can be included as a client-side script for automatically generating random images whenever an image element has `hhhhold.js/` in the `src` attribute.  This allows various parameters to be passed to hhhhold, like the size of the image, or other options such as image brightness.

###w2ui

![w2ui](/images/posts/w2ui.png)

w2ui (GitHub: [vitmalina / w2ui](https://github.com/vitmalina/w2ui), License: _MIT_) by Vitali Malinouski is a UI library that is designed to be used with jQuery.  The site has demos which use Bootstrap, but it doesn't actually depend on Bootstrap as such -- the project's CSS files have been designed to work alongside other CSS libraries.  There's also a [w2ui demo page](http://w2ui.com/web/demos/#!sidebar/sidebar-1) that shows what the various widgets look like without Bootstrap.

So, what's included?  There are some widgets I find myself needing for a lot of projects that don't come with Bootstrap, like sidebars and the data grid.  There are also utility functions for validating values base64 encoding and decoding.

The JavaScript is all namespaced in `w2utils` and `w2ui`, and the CSS styles all have a `w2ui-` prefix, so it should be easy to drop it into a project to see what the widgets look like alongside existing functionality.

###Event Spy

[Event Spy](http://event-spy.blogspot.dk/) (Google Code: [event-spy](http://code.google.com/p/event-spy/), License: _New BSD_, Chrome Web Store: [Event Spy](https://chrome.google.com/webstore/detail/event-spy/jhicediiohboeebfbhllbdhlghmbgbol)) by Johan Laursen is a Chrome extension that adds event tracking to the developer tools.  Only events with a listener will be displayed, and the target will be highlighted on the page.

The Chrome Web Store page for the project has a video that demonstrates the plugin in action, along with screenshots.
