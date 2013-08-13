---
layout: post
title: "jQuery Roundup: jQuery.emphasis.js, Tipue Search"
author: Alex Young
categories:
- jquery
- plugins
- iframes
- css3
- internationalization
- languages
---

<div class="intro">
Note: You can send your plugins and articles in for review through our <a href="http://contact.dailyjs.com/project">contact form</a>.
</div>

###jQuery.emphasis.js

[jQuery.emphasis.js](http://nodejs.in/jquery.emphasis/) (GitHub: [zmmbreeze / jquery.emphasis](https://github.com/zmmbreeze/jquery.emphasis), License: _MIT_, jQuery: [emphasis](http://plugins.jquery.com/emphasis/)) by "mzhou" is a CSS3 `text-emphasis` fallback.

The author says it's useful for East Asian languages because it adds symbols above or below characters to improve the clarity of emphasised sections.  The equivalent CSS currently only works in WebKit with a vendor prefix, so this plugin will be useful to those working with these languages.

[The source is quite interesting](https://github.com/zmmbreeze/jquery.emphasis/blob/master/src/jquery.emphasis.js) -- it's based on the CSS3 specification, which involves determining if a character is suitable for emphasis, then the insertion of fairly complex styles to simulate the emphasis marks.

###Tipue Search

![Tipue image search](/images/posts/tipue.png)

[Tipue Search](http://www.tipue.com/search/) (License: _MIT_) is a site search plugin.  It can search static JSON content, or pages on the same origin using Ajax.  It also supports an image search mode, which looks for matches in JSON content that points to image URLs.

Given an index, like this:

{% highlight javascript %}
var tipuesearch = {"pages": [
  {"title": "Tipue Search, a site search engine jQuery plugin", "text": "Tipue Search is a site search engine jQuery plugin. Tipue Search is open source and released under the MIT License, which means it's free for both commercial and non-commercial use. Tipue Search is responsive and works on all reasonably modern browsers.", "tags": "JavaScript", "loc": "http://www.tipue.com/search"},
  {"title": "Tipue drop, a search suggestion box jQuery plugin", "text": "Tipue drop is a search suggestion box jQuery plugin. Tipue drop is open source and released under the MIT License, which means it's free for both commercial and non-commercial use. Tipue drop is responsive and works on all reasonably modern browsers.", "tags": "JavaScript", "loc": "http://www.tipue.com/drop"},
  {"title": "About Tipue", "text": "Tipue is a small web development studio based in North London. We've been around for over a decade. We like minimalism with the occasional hint of retro.", "tags": "", "loc": "http://www.tipue.com/about"}
]};
{% endhighlight %}

Tipue can be enabled using `$('#tipue_search_input').tipuesearch();` on a suitable `input` element.

###Auto Iframe Height Plugin Update

Ilker Guller updated his [Auto Iframe Height Plugin](http://sly777.github.io/Iframe-Height-Jquery-Plugin/) (GitHub: [Sly777 / Iframe-Height-Jquery-Plugin](https://github.com/Sly777/Iframe-Height-Jquery-Plugin), License: _MIT, GPL_) to automatically check the iframe height when the contents change.

To enable automatic resizing, you can use the `watcher` option passed to `$.iframeHeight`.  It also supports several other options, including: `defaultHeight`, `minimumHeight`, and `watcherTime`.


