---
layout: post
title: "Script Roundup: Dolly.js, ngProgress"
author: Alex Young
categories:
- jquery
- plugins
- angular
---

<div class="intro">
Note: You can send your scripts and articles in for review through our <a href="/contact.html">contact form</a>.
</div>

###Dolly.js

[Dolly.js](http://lunarlogic.github.io/dolly.js/) (GitHub: [LunarLogic / dolly.js](https://github.com/LunarLogic/dolly.js), License: _MIT_) from Lunar Logic is a jQuery UI widget for cloning fields in tables.  It works like Excel and does not make any assumptions about the underlying data structure.  Rows and cells can be constrained with selectors, and the API is event-based so you can hook up listeners to `cloned` events.

{% highlight javascript %}
$(cell).dolly({
  rowSelector: 'div.row',
  cellSelector: 'div.cell'
});
{% endhighlight %}

###ngProgress

[ngProgress](http://labs.voronianski.com/ngprogress-lite.js/) (GitHub: [voronianski / ngprogress-lite](https://github.com/voronianski/ngprogress-lite), License: _MIT_) by Dmitri Voronianski is a port of [NProgress](https://github.com/rstacruz/nprogress/) for AngularJS applications.  NProgress looks like the Chrome for Android progress bar which is a glowing blue line that grows to fill the top of the page.

The ngProgress demo page allows you to see how it works with buttons for each API call, for example: `.set(0.4)` and `.inc()`.  This is the perfect way to give people feedback when your AngularJS app makes Ajax requests to the server.

