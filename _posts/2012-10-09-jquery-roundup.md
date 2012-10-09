---
layout: post
title: "jQuery Roundup: jQuery UI 1.9.0, Delta Theme, jQuery.textFit"
author: Alex Young
categories:
- jquery
- jquery-ui
- plugins
- themes
---

<div class="intro">
Note: You can send your plugins and articles in for review through our <a href="/contact.html">contact form</a> or <a href="http://twitter.com/dailyjs">@dailyjs</a>.
</div>

###jQuery UI 1.9.0

![jQuery UI 1.9.0 site](/images/posts/jquery-ui-190.png)

[jQuery UI 1.9.0](http://blog.jqueryui.com/2012/10/jquery-ui-1-9-0/) is out, which adds new widgets, API refinements, improved accessibility, and hundreds of bug fixes.  The new widgets are as follows:

* [Menu](http://api.jqueryui.com/menu/): A navigation menu with support for hierarchical pop-up submenus
* [Spinner](http://api.jqueryui.com/spinner/): A "number stepper" for input fields (rather than a rotating progress indicator)
* [Tooltip](http://jqueryui.com/tooltip/): A pop-up message

There's a detailed [jQuery UI 1.9 Upgrade Guide](http://jqueryui.com/upgrade-guide/1.9/#api-redesigns) which lists deprecations.  Oh, and the jQuery UI site has been refreshed as well!

###Delta: jQuery UI Theme

![jQuery UI Delta Theme](/images/posts/jquery-ui-delta.png)

[Delta](http://blog.kiandra.com.au/2012/09/delta-a-free-jquery-ui-theme/) (GitHub: [kiandra / Delta-jQuery-UI-Theme](https://github.com/kiandra/Delta-jQuery-UI-Theme), License: _MIT/GPL_) is a jQuery UI theme by Tait Brown, who created the hugely popular [Aristo port](http://taitems.github.com/Aristo-jQuery-UI-Theme/).

This theme has a metallic finish that reminds me if iOS 6, and includes light and dark variations.  It's also dubbed as _Retina ready_ -- CSS3 gradients and high-resolution images have been used.

###jQuery.textFit

[jQuery.textFit](http://strml.github.com/examples/jquery.textFit.html) (GitHub: [STRML / jquery.textFit](https://github.com/STRML/jquery.textFit), License: _MIT_) by Samuel Reed can scale text to fit its container.  It also correctly detects multiline strings with break tags.

To find the best font size, a binary search is performed.  The demo on jQuery.textFit's site is slowed down so you can actually see how the algorithm works, in reality it seems to run very quickly.

Vertical alignment and centred text are both supported, as are custom fonts.
