---
layout: post
title: "jQuery Roundup: jQuery-menu-aim, Toolbar, ngInfiniteScroll"
author: Alex Young
categories:
- jquery
- plugins
- usability
- menus
- toolbars
- pagination
---

<div class="intro">
Note: You can send your plugins and articles in for review through our <a href="/contact.html">contact form</a>.
</div>

###jQuery-menu-aim

jQuery-menu-aim (GitHub: [kamens / jQuery-menu-aim](https://github.com/kamens/jQuery-menu-aim), License: _MIT_) by Ben Kamens is a for making large dropdowns in a similar style to Amazon.  Ben has written a post about why this is desirable: [Breaking Down Amazon's Mega Dropdown](http://bjk5.com/post/44698559168/breaking-down-amazons-mega-dropdown).

> At every position of the cursor you can picture a triangle between the current mouse position and the upper and lower right corners of the dropdown menu. If the next mouse position is within that triangle, the user is probably moving their cursor into the currently displayed submenu. Amazon uses this for a nice effect. As long as the cursor stays within that blue triangle the current submenu will stay open 

Ben made a diagram of this to visualise the area used to detect the mouse.

![jQuery-menu-aim](/images/posts/amazon-hover-area.png)

I thought this was a great piece of work, both from the developers at Amazon and Ben in recognising something interesting was going on behind the scenes.  The plugin comes with an example, and has configuration options for integrating it with your existing markup.

###Toolbar

![Toolbar](/images/posts/toolbarsjs2.png)

[Toolbar](http://paulkinzett.github.com/toolbar/) (GitHub: [paulkinzett / toolbar](https://github.com/paulkinzett/toolbar), License: _MIT_, jQuery: [toolbar](http://plugins.jquery.com/toolbar/)) by Paul Kinzett is a plugin for quickly creating popup toolbars with icons.  The markup is an unordered list, and the toolbar can be oriented both vertically and horizontally.

The plugin includes CSS and icons, so it can be dropped straight into a project and should look similar to the examples on the site.

###ngInfiniteScroll

[ngInfiniteScroll](http://binarymuse.github.com/ngInfiniteScroll/) (GitHub: [BinaryMuse / ngInfiniteScroll](https://github.com/BinaryMuse/ngInfiniteScroll), License: _MIT_, npm: [ng-infinite-scroll](https://npmjs.org/package/ng-infinite-scroll)) is an AngularJS project that depends on jQuery which can help implement infinite scrolling.  It's used by adding the `infinite-scroll` attribute to an element, and then implementing a controller that can fetch data when required.

The [remote data demo](http://binarymuse.github.com/ngInfiniteScroll/demo_async.html) shows how it works by calling Reddit's JSONP API.

