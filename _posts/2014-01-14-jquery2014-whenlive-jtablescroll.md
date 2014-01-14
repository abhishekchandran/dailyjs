---
layout: post
title: "The State of jQuery, jQuery.whenLive, jTableScroll"
author: Alex Young
categories:
- jquery
- plugins
---

###The State of jQuery 2014

[The State of jQuery 2014](http://blog.jquery.com/2014/01/13/the-state-of-jquery-2014/) was posted to the jQuery blog yesterday by Dave Methvin.  It basically covers jQuery's growth through 2013, and includes a comment about how jQuery shouldn't just be used for routing around broken DOM APIs:

> People should be continuing to use jQuery because it's a powerful way to implement designs and provides a vibrant ecosystem of useful plugins, not because the native DOM APIs are broken, verbose, or inconsistent. That's why we participate in the standards process through bodies such as the W3C and ECMA.

###jQuery.whenLive

[jQuery.whenLive](http://bitcubby.com/tracking-the-insertion-of-javascript-components-into-the-dom/) (GitHub: [tkambler / whenLive](https://github.com/tkambler/whenLive), License: _MIT_, Bower: `tkambler/whenLive`) by Tim Ambler allows you to track when elements are inserted into the DOM tree, with a focus on performance:

> When supported, $.whenLive leverages the browser’s MutationObserver notification system. In the event that Mutation Observers are unavailable, $.whenLive leverages the relatively new requestAnimationFrame function.

This seems like a clever way of deferring behaviour until potentially complex components are ready.

###jTableScroll

[jTableScroll](http://mikeallisononline.com/Projects/jTableScroll) (GitHub: [mike-allison / jTableScroll](https://github.com/mike-allison/jTableScroll), License: _MIT_) by Mike Allison is a plugin for adding scrollbars to tables, and it retains static headers and footers.

It calculates the width and height then wraps parts of the table in divs, applying the necessary `overflow` styles based on size options: `$('#tableToScroll').jTableScroll({ width: 300, height: 300 })`.

The header and footer are cloned and moved by looking for the `thead` and `tbody` elements, so you'll need a well-structured table.  It can be installed with [nuget](https://www.nuget.org/packages/jTableScroll/).
