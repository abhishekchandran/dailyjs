---
layout: post
title: "jQuery 2.0 Released"
author: Alex Young
categories:
- jquery
- plugins
---

<div class="intro">
Note: You can send your plugins and articles in for review through our <a href="/contact.html">contact form</a>.
</div>

[jQuery 2.0](http://blog.jquery.com/2013/04/18/jquery-2-0-released/) has been released.  The most significant, headline-grabbing change is the removal of support for legacy browsers, including IE 6, 7, and 8.  The 1.x branch will continue to be supported, so it's safe to keep using it if you need broad IE support.

The [jquery-migrate](https://github.com/jquery/jquery-migrate/#readme) plugin can be used to help you migrate away from legacy APIs.  jQuery 2.0 is "API compatible" with 1.9, which means migration shouldn't be as painful as it could be.  They've been pushing jquery-migrate for a while now, so hopefully this stuff isn't new to anyone who likes to keep current with jQuery.

The announcement blog post has more details on IE support, the next release of jQuery, and the benefits of upgrading to 2.0.

###Upgrade Planning

If you're interested in upgrading, the [jQuery documentation](http://api.jquery.com/) has notes on each API method that is deprecated.  It also documents features that can be used to mitigate API changes -- for example, if you're using a plugin that requires an earlier version of jQuery, you could technically run multiple versions on a page by using [jQuery.noConflict](http://api.jquery.com/jQuery.noConflict/):

{% highlight html %}
<script type="text/javascript" src="other_lib.js"></script>
<script type="text/javascript" src="jquery.js"></script>
<script type="text/javascript">
  $.noConflict();
  // Code that uses another library's $ can follow here.
</script>
{% endhighlight %}

Plugins that are listed on [the jQuery Plugin Registry](http://plugins.jquery.com/) _should_ list the required jQuery version in the [package manifest file](http://plugins.jquery.com/docs/package-manifest/#field-dependencies).  That means you can easily see what version of jQuery a plugin depends on.  Many already do depend on jQuery 1.9 or above, so they should be safe to use with jQuery 2.0.

As always, well-tested projects should be easier to migrate.  So get those QUnit tests out and see what happens!
