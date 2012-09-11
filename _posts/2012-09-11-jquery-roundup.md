---
layout: post
title: "jQuery Roundup: jQuery License Change, FileUploader, Raphaël Tutorial"
author: Alex Young
categories:
- jquery
- plugins
- raphael
- file
---

<div class="intro">
Note: You can send your plugins and articles in for review through our <a href="/contact.html">contact form</a> or <a href="http://twitter.com/dailyjs">@dailyjs</a>.
</div>

###jQuery Now MIT Licensed

jQuery was previously dual licensed under the MIT and GPL.  This shouldn't technically change anything, because the work could be relicensed under the GPL if required:

> Having just one license option makes things easier for the Foundation to manage and eliminates confusion that existed about the Foundation's previous dual-licensing policy. However, this doesn't affect your ability to use any of the Foundation's projects. You are still free to take a jQuery Foundation project, make changes, and re-license it under the GPL if your situation makes that desirable.

Contributors are being asked to sign a license agreement to ensure everything published under the jQuery Foundation has the necessary legal background.  The license agreement has been modeled on the [Contributor Agreements](http://wiki.civiccommons.org/Contributor_Agreements) for copyright assignment, published by the Civic Commons Community.

###FileUploader

[FileUploader](https://github.com/valums/file-uploader) (License: _MIT/GPL2/LGPL2_) by Andrew Valums and Ray Nicholus is a [File API](http://dev.w3.org/2006/webapi/FileAPI/) wrapper.  It can handle multiple uploads by using XMLHttpRequest, and will fall back to an iframe-based solution in older browsers.  The API looks like this:

{% highlight javascript %}
var uploader = new qq.FileUploader({
  // pass the dom node (ex. $(selector)[0] for jQuery users)
  element: document.getElementById('file-uploader'),

  // path to server-side upload script
  action: '/server/upload'
});
{% endhighlight %}

It doesn't have any external dependencies, and has many advanced features, including drag-and-drop file selection, multiple uploads, and keyboard support.

###Raphaël Tutorial

[Making a Simple Drawing Application using RaphaëlJS](http://lynx.io/article/simple-drawing-application-raphaeljs) is a tutorial by Callum Macrae that uses Raphaël and jQuery to create a simple paint program.  It includes a basic introduction to Raphaël, and uses jQuery-based event handling to create the mouse-driven drawing interface.

