---
layout: post
title: "jQuery Roundup: jQuery 1.8, BBSearch, MDMagick, Document-Bootstrap, DownloadBuilder.js"
author: Alex Young
categories: 
- jquery
- plugins
- backbone.js
- sessionStorage
- files
---

<div class="intro">
Note: You can send your plugins and articles in for review through our <a href="/contact.html">contact form</a> or <a href="http://twitter.com/dailyjs">@dailyjs</a>.
</div>

###jQuery 1.8

[jQuery 1.8](http://blog.jquery.com/2012/08/09/jquery-1-8-released/) has been released.  jQuery 1.8 makes some fairly significant changes:

* The selector engine has been rewritten
* [Animations have been reworked](https://gist.github.com/54829d408993526fe475)
* `.css` and `.animate` will automatically add vendor prefixes
* The size has been reduced compared to jQuery 1.7.2
* Grunt build system

###BBSearch

[BBSearch](http://fguillen.github.com/BBSearch/) (GitHub: [fguillen / BBSearch](https://github.com/fguillen/BBSearch), License: _CC BY 3.0_) by Fernando Guillen is a find-as-you-type style plugin that's designed to work with Backbone.js.  It can also work with JSONP APIs, and the author has included demos that use GitHub and Twitter.

{% highlight javascript %}
$('#search-input-1').bbsearch({
  url: 'https://api.github.com/legacy/repos/search/#bbsearch-query#?callback=?&'
, itemTemplate: '<p>[@<%= owner %>] <a href="<%= url %>"><%= name %></a></p>'
, resultsElement: $('#results-1')
, parse: function(response) { return response.data.repositories; }
});
{% endhighlight %}

###MDMagick

![MDMagick](/images/posts/mdmagick.png)

[MDMagick](http://fguillen.github.com/MDMagick/) (GitHub: [fguillen / MDMagick](https://github.com/fguillen/MDMagick), License: _CC BY 3.0_) also by Fernando Guillen is a Markdown interface for jQuery.  It uses [Showdown](https://github.com/coreyti/showdown/), which is a Markdown parser for JavaScript, and [a-tools](http://archive.plugins.jquery.com/project/a-tools) for handling text selections.

###Document-Bootstrap and DownloadBuilder.js

[Document-Bootstrap](http://gregfranko.com/Document-Bootstrap/) (GitHub: [gfranko / Document-Bootstrap](https://github.com/gfranko/Document-Bootstrap), License: _MIT_) by Greg Franko is a boilerplate for creating responsive Bootstrap projects.  It also includes [DownloadBuilder.js](http://gregfranko.com/DownloadBuilder.js/) (GitHub: [gfranko / DownloadBuilder.js](https://github.com/gfranko/DownloadBuilder.js), License: _MIT_), a project by the same author that uses the HTML5 File API to create optimised client-side scripts.

DownloadBuilder.js supports concatenating local files and files hosted on GitHub.  It can also cache Ajax/JSONP requests by using `sessionStorage`.
