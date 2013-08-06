---
layout: post
title: "jQuery Roundup: spy-js, yadcf"
author: Alex Young
categories:
- jquery
- plugins
- sponsored-content
- services
- tables
- ui
---

<div class="intro">
Note: You can send your plugins and articles in for review through our <a href="http://contact.dailyjs.com/project">contact form</a>.
</div>

###spy-js

<div class="sponsored-content">
  <p><a class="label" href="/sponsored-content.html">Sponsored Content</a> This jQuery Roundup is sponsored by spy-js.</p>
</div>

<div class="image">
  <img src="/images/posts/spyjs.png" alt="" />
  <small>spy-js.</small>
</div>

[spy-js](http://spy-js.com/), created by [Artem Govorov](https://twitter.com/ArtemGovorov), is a commercial tool that aims to make JavaScript instrumentation better.  You can use it to trace, debug, and profile code that would otherwise be difficult to work with.

Although tools like Chrome DevTools are excellent, the advantage of spy-js is it can work with any browser.  It also allows performance _between_ browsers to be compared more easily.

<div class="image">
  <img src="/images/posts/spyjss.png" alt="" />
  <small>spy-js in action.</small>
</div>

There's a free beta which you can download from [spy-js.com](http://spy-js.com), and [issues are being tracked on GitHub](https://github.com/spy-js/spy-js/issues).  The documentation is also on GitHub, at [spy-js/spy-js](https://github.com/spy-js/spy-js/issues).  The project isn't open source, but the author intends to keep it free while he collects beta feedback.

For more information, take a look at [spy-js.com](http://spy-js.com/) and [@SpyDashJs](https://twitter.com/SpyDashJs) on Twitter.

###yadcf

[Yet Another DataTables Column Filter](http://yadcf-showcase.appspot.com) (GitHub: [vedmack / yadcf](https://github.com/vedmack/yadcf), License: _GPL2/BSD_, jQuery: [yadcf](http://plugins.jquery.com/yadcf/)) by Daniel Reznick is a plugin for [DataTables](https://datatables.net) that adds filtering components.  It can filter based on a `select`, or the jQuery UI Autocomplete widget.  It also parses different data types, like delimited plain text and HTML elements.

{% highlight javascript %}
$(document).ready(function(){
  $('#example').dataTable().yadcf([
    { column_number: 0 },
    { column_number: 1, filter_container_id: 'external_filter_container' },
    { column_number: 2, data:['Yes', 'No'], filter_default_label: 'Select Yes/No' },
    { column_number: 3, text_data_delimiter: ',', enable_auto_complete: true },
    { column_number: 4, column_data_type: 'html', html_data_type: 'text', filter_default_label: 'Select tag' }]);
});
{% endhighlight %}

It also works perfectly well with multiple tables on a page.  For more examples, check out the [yadcf showcase](http://yadcf-showcase.appspot.com/) and the project's readme.
