---
layout: post
title: "Node Roundup: 0.10.4, Papercut, rsz, sz"
author: "Alex Young"
categories: 
- node
- modules
- graphics
- images
- uploads
---

<div class="intro">
You can send in your Node projects for review through our <a href="/contact.html">contact form</a>.
</div>

###Node 0.10.4

[Node 0.10.4](http://blog.nodejs.org/2013/04/11/node-v0-10-4-stable/) was released last week.  There are bug fixes for some core modules, and I also noticed this:

> v8: Avoid excessive memory growth in JSON.parse (Fedor Indutny)

Another interesting patch was added to the stream module, to ensure `write` callbacks run before `end`:

[stream: call write cb before finish event](https://github.com/joyent/node/commit/c93af860a079654becb3b1d06184ab7428dedffb)

The Node blog was quietly updated to change the latest 0.8 to read "legacy" instead of "stable".  I don't recall previous stable releases being referred to in this way before, so I thought it was worth mentioning here.

###Papercut

Papercut (GitHub: [Rafe / papercut](https://github.com/Rafe/papercut), License: _MIT_, npm: [papercut](https://npmjs.org/package/papercut)) by Jimmy Chao is an image uploading module that supports Amazon S3 and resizing and cropping through [node-imagemagick](https://npmjs.org/package/imagemagick).

Uploaders can be created according to a schema, allowing them to be used to manage different aspects of your application's image handling requirements:

{% highlight javascript %}
AvatarUploader = papercut.Schema(function(schema){
  schema.version({
    name: 'avatar'
  , size: '200x200'
  , process: 'crop'
  });

  schema.version({
    name: 'small'
  , size: '50x50'
  , process: 'crop'
  });
});
{% endhighlight %}

Papercut also supports configuration using `NODE_ENV`, so it's easy to configure to work sensibly in various deployment environments.

###rsz

rsz (GitHub: [rvagg / node-rsz](https://github.com/rvagg/node-rsz), License: _MIT_, npm: [rsz](https://npmjs.org/package/rsz)) by Rod Vagg is a module for resizing images based on LearnBoost's [node-canvas](https://github.com/LearnBoost/node-canvas).  The API is based around a single method which accepts various signatures.  The basic usage is `rsz(src, width, height, function (err, buf) { /* */ })`.

###sz

sz (GitHub: [rvagg / node-sz](https://github.com/rvagg/node-sz), License: _MIT_, npm: [sz](https://npmjs.org/package/sz)), also by Rod, is another image-related module.  This one can determine the size of an image.  It should be noted that both of these modules work with image files and `Buffer` objects.

{% highlight javascript %}
var buf = fs.readFileSync('image.gif');

sz(buf, function(err, size) {
  // where `size` may look like: { height: 280, width: 400 }
});
{% endhighlight %}

