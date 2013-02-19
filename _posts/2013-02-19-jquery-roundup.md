---
layout: post
title: "jQuery Roundup: Durandal, Version.js, Navi.js"
author: Alex Young
categories:
- jquery
- plugins
- frameworks
- libraries
- testing
- navigation
---

<div class="intro">
Note: You can send your plugins and articles in for review through our <a href="/contact.html">contact form</a>.
</div>

###Durandal

[Durandal](http://durandaljs.com/) (GitHub: [BlueSpire / Durandal](https://github.com/BlueSpire/Durandal/), License: _MIT_) combines jQuery, Knockout, and RequireJS with some of its own code to create a framework for developing single page applications.  Durandal apps are built using AMD-based modules, and it also supports the notion of a [widget](http://durandaljs.com/documentation/Creating-A-Widget.html).

One interesting feature is [application-wide messaging](http://durandaljs.com/documentation/Leveraging-Publish-Subscribe.html) -- the main `app` object can handle events, so it can be used as a universal message bus to help keep functionality nicely decoupled.

The project includes Jasmine/PhantomJS tests in the [test/](https://github.com/BlueSpire/Durandal/tree/master/test) directory, but the documentation itself doesn't mention tests and the application skeletons don't include them either.  That seems like an oversight to me, given that the project claims to be "single page apps done right".

###Version.js

Justin Stayton sent in Version.js ([jstayton / version.js](https://github.com/jstayton/version.js), License: _MIT_, bower: _version.js_), which he developed while testing scripts against multiple versions of jQuery.  It works by using attributes to specify the required versions of libraries:

{% highlight html %}
<script src="version.js" data-url="google" data-lib="jquery" data-ver="1.7.2"></script>
{% endhighlight %}

This will cause jQuery 1.7.2 to be loaded from Google's CDN as the default.  If another version is required, the `versionjs` GET parameter can be used.  This makes it easy to switch between versions of a dependency, which might be useful in tests or during local development.

###Navi.js

[Navi.js](http://navi.grantcr.com) (GitHub: [tgrant54 / Navi.js](https://github.com/tgrant54/Navi.js), License: _MIT_) by Tyler Grant makes single pages behave like a full site using hash routing.  It has breadcrumb support, and can be called multiple times.  The jQuery plugin method takes a `hash` option so you could embed multiple menus on a page, each using a different hash to distinguish between them:

{% highlight javascript %}
$('#naviMenu').navi({
  hash: '#!/'
, content: $('#naviContent')
});
{% endhighlight %}

The project's homepage has markup samples and demos.
