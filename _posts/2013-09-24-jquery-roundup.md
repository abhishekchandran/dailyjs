---
layout: post
title: "jQuery Roundup: 2.1 Beta, dna.js"
author: Alex Young
categories:
- jquery
- plugins
- templates
---

<div class="intro">
Note: You can send your plugins and articles in for review through our <a href="/contact.html">contact form</a> or <a href="http://twitter.com/dailyjs">@dailyjs</a>.
</div>

###jQuery 1.11 and 2.1 Beta 1

[jQuery 1.11 and 2.1 Beta 1](http://blog.jquery.com/2013/09/19/jquery-1-11-and-2-1-beta-1-released/) have been released.  The biggest news is jQuery now supports AMD, and is built with it.  Internal dependencies are also managed with Bower.

By using AMD and Bower the jQuery developers are showing that they're receptive to the needs of modern client-side developers.  

###dna.js

[dna.js](http://dnajs.org/) (GitHub: [dnajs / dna.js](https://github.com/dnajs/dna.js), License: _GPLv3/MIT_, jQuery: [dna](http://plugins.jquery.com/dna/)) by Dem Pilafian is a template library that uses valid HTML rather than a new syntax or inline JavaScript templates.  It clones an element as many times as you need, and interpolates values.

A template looks like this:

{% highlight html %}
<div>
  <h2>Featured Books</h2>
  <div id="book" class="dna-template">
    <div>Title:  <span>~~title~~</span></div>
    <div>Author: <span>~~author~~</span></div>
  </div>
</div>
{% endhighlight %}

And you can clone it with `dna.clone('book', { title: 'The DOM', author: 'Jan' })`.

