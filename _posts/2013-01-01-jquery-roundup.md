---
layout: post
title: "jQuery Roundup: jKit, ZinoUI, jQuery.ajax.fake"
author: Alex Young
categories:
- jquery
- plugins
- frameworks
- ui
- ajax
- testing
---

<div class="intro">
Note: You can send your plugins and articles in for review through our <a href="/contact.html">contact form</a> or <a href="http://twitter.com/dailyjs">@dailyjs</a>.
</div>

###jKit

<div class="image">
  <img src="/images/posts/jkit.png" alt="" />
  <small>jKit's site includes demos of every effect and component.</small>
</div>

[jKit](http://jquery-jkit.com/) (GitHub: [FrediBach / jQuery-jKit](https://github.com/FrediBach/jQuery-jKit), License: _MIT_) by Fredi Bach is a relatively small (47 KB) UI toolkit.  It can work with data attributes, so adding `data-jkit` attributes to the relevant elements will invoke various components.

There are a lot of effects and components, including tooltips, charts, parallax scrolling, and a lightbox.  The project has detailed documentation on each of the bundled plugins, and [a simple introduction for non-programmers](http://jquery-jkit.com/pages/basics.php).

###ZinoUI

<div class="image">
  <img src="/images/posts/zinotree.png" alt="" />
  <small>The ZinoUI TreeView component.</small>
</div>

Coincidentally, Dimitar Ivanov also sent in a UI toolkit of sorts: the [ZinoUI Framework](http://zinoui.com/) (License: [CC BY-NC 3.0](http://zinoui.com/license)).  This framework requires commercial licensing starting at $50 per site, and includes advanced widgets more comparable to jQuery UI, like a calendar and tree view.

ZinoUI is [WAI-ARIA](http://www.w3.org/WAI/intro/aria.php) compatible, so may suit projects with stricter accessibility requirements.  It has been tested with Google Chrome 12+, Firefox 4+, Safari 5+, Opera 11+, and IE8+.

###jQuery.ajax.fake

[jQuery.ajax.fake](http://anasnakawa.github.com/jquery.ajax.fake/) (GitHub: [anasnakawa / jquery.ajax.fake](https://github.com/anasnakawa/jquery.ajax.fake), License: _MIT_, component: `anasnakawa/jquery.ajax.fake`) by Anas Nakawa can be used to mock jQuery `$.ajax` calls.  A mocked call will be made when passing `fake: true` as an option to `$.ajax`.  It can be disabled globally, and works with deferred calls.

