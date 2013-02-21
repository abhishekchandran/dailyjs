---
layout: post
title: "Cloudinary Tutorial"
author: Alex Young
categories:
- node
- tutorials
- jquery
- images
- graphics
- services
- sponsored-content
---

<div class="sponsored-content">
  <p><a class="label" href="/sponsored-content.html">Sponsored Content</a> This post is about a commercial product that we think will appeal to DailyJS readers.</p>
</div>

###Cloudinary

![Cloudinary](/images/posts/cloudinary.png)

This tutorial introduces [Cloudinary](http://cloudinary.com/), and demonstrates how to build a gallery application using Express and Node.  Cloudinary is a service for streamlining asset management -- if you're tired of optimising images and manually uploading them to an asset server or CDN, then Cloudinary might be what you're looking for.

One reason Cloudinary is useful to us as Node developers is the Cloudinary Node module (GitHub: [cloudinary / cloudinary_npm](https://github.com/cloudinary/cloudinary_npm), License: _MIT_, npm: [cloudinary](https://npmjs.org/package/cloudinary)).  It can be used to easily generate optimised images, thumbnails, and automatically upload them to Cloudinary.  Let's drop it into an Express application to see what happens!

The full source for this tutorial is available here: [alexyoung / dailyjs-cloudinary-gallery](https://github.com/alexyoung/dailyjs-cloudinary-gallery).

###Step 1: Create a Cloudinary Account

Register for a [free account at Cloudinary](http://cloudinary.com/plans).  That'll give you 500 MB of storage and a gigabyte of monthly bandwidth.  Paid plans start at $39 a month, and that increases the storage to 10 GB and adds 40 GB a month of bandwidth.

Once you've created your account, sign in and take a look at the right-hand panel that reads "Account Details".

<div class="image">
  <img src="/images/posts/cloudinary-1.png" />
  <small>The Cloudinary management interface.</small>
</div>

To follow this tutorial, you'll need the `api_key` and `api_secret`, so make a note of those.

###Step 2: The Express App

Assuming you've already installed [Node](http://nodejs.org/), open a terminal and run `npm install -g express`.  Once that's done, run `express dailyjs-cloudinary-gallery` to create a new Express project.

Open `package.json` and add the `cloudinary` dependency:

{% highlight javascript %}
{
  "name": "application-name",
  "version": "0.0.1",
  "private": true,
  "scripts": {
    "start": "node app"
  },
  "dependencies": {
    "express": "3.0.3",
    "jade": "*",
    "cloudinary": "*"
  }
}
{% endhighlight %}

Once you've done that, save the file and run `npm install`.  This will install the project's dependencies, including the Cloudinary module.

###Step 3: Image Uploads

Cloudinary can be used for every aspect of an image gallery:

* Uploading images
* Creating and serving thumbnails
* Fetching a list of images to display

Go to the top of `app.js` and add the following `require` statements:

{% highlight javascript %}
var cloudinary = require('cloudinary')
  , fs = require('fs')
{% endhighlight %}

Now add a new route to handle uploads:

{% highlight javascript %}
app.post('/upload', function(req, res){
  var imageStream = fs.createReadStream(req.files.image.path, { encoding: 'binary' })
    , cloudStream = cloudinary.uploader.upload_stream(function() { res.redirect('/'); });

  imageStream.on('data', cloudStream.write).on('end', cloudStream.end);
});
{% endhighlight %}

Add your Cloudinary configuration to `app.configure`:

{% highlight javascript %}
app.configure('development', function(){
  app.use(express.errorHandler());
  cloudinary.config({ cloud_name: 'yours', api_key: 'yours', api_secret: 'yours' });
});

app.locals.api_key = cloudinary.config().api_key;
app.locals.cloud_name = cloudinary.config().cloud_name;
{% endhighlight %}

This allows you to use different Cloudinary accounts for development and production purposes, depending on your requirements.

The last two lines make the values available to the templates.  The secret is not meant to be accessible from outside the server, but the `api_key` and `cloud_name` options can be used by client-side scripts.

Change `views/index.jade` to show an upload form:

{% highlight text %}
extends layout

block content
  h1= title
  p Welcome to #{title}

  form(action="/upload", method="post", enctype="multipart/form-data")
    input(type="file", name="image")
    input(type="submit", value="Upload Image")

  - if (images && images.length)
    - images.forEach(function(image){
      img(src=image.url)
    - })
{% endhighlight %}

Before you try out the app, change the `/` route in `app.js` to load a set of images from Cloudinary:

{% highlight javascript %}
app.get('/', function(req, res, next){
  cloudinary.api.resources(function(items){
    res.render('index', { images: items.resources, title: 'Gallery' });
  });
});
{% endhighlight %}

The `cloudinary.api.resources` method fetches all of the images in your account.  Note that this is rate limited to 500 requests per hour -- I've used it here to keep the tutorial simple, but in production you should cache the results or store them in a database.

At this point, image uploads should work if you start up the app with `npm start` and navigate to [http://localhost:3000](http://localhost:3000), but the output won't look great without thumbnails.

###Step 4: Thumbnails

Cloudinary supports a wide range of [image transformations](http://cloudinary.com/documentation/image_transformations).  The API is based around generating a URL that includes parameters to change the image in some way.  All we need for the gallery is a simple crop, which is supported through the `cloudinary.url` method.  Change the `/` route to pass a reference to the `cloudinary` object to the template:

{% highlight javascript %}
app.get('/', function(req, res, next){
  cloudinary.api.resources(function(items){
    res.render('index', { images: items.resources, title: 'Gallery', cloudinary: cloudinary });
  });
});
{% endhighlight %}

Now, open `views/index.jade` so that it calls `cloudinary.url` with some options to get the desired effect:

{% highlight text %}
- images.forEach(function(image){
  a(href=image.url)
    img(src=cloudinary.url(image.public_id + '.' + image.format, { width: 100, height: 100, crop: 'fill', version: image.version }))
- })
{% endhighlight %}

The important part here is this:

{% highlight javascript %}
cloudinary.url(image.public_id + '.' + image.format, { width: 100, height: 100, crop: 'fill', version: image.version })
{% endhighlight %}

The `cloudinary.url` method generates a URL that includes the width, height, and crop options:

{% highlight text %}
http://res.cloudinary.com/your_account/image/upload/c_fill,h_100,w_100/v1234/file.jpg
{% endhighlight %}

Because the API is based around URLs, you could easily use this from browser-based JavaScript, utilising Cloudinary to add behaviour that would typically be associated with server-side web development.

I've also included the `version` property, which is recommended by Cloudinary when overriding the `public_id`.  It's returned by both the upload API and the admin API.

###Step 5: Effects

The previous example can easily be adapted to generate lots of interesting effects.  This change makes it generate images that feature a vignette lens effect:

{% highlight text %}
- images.forEach(function(image){
  a(href=image.url)
    img(src=cloudinary.url(image.public_id + '.' + image.format, { width: 100, height: 100, crop: 'fill', effect: 'vignette', version: image.version }))
- })
{% endhighlight %}

The `effect` parameter can be one of the following effects:

* grayscale
* blackwhite
* vignette
* sepia
* brightness
* saturation
* contrast
* hue
* pixelate
* blur
* sharpen

Some effects take an argument, and this is simply prefixed with a colon.  For example, `brightness:40`.

As well as face detection, adding rounded corners, overlays, and other transformations are also available.  Again, check the [image transforms](http://cloudinary.com/documentation/image_transformations) documentation for full details.

<div class="image">
  <img src="/images/posts/cloudinary-effects.png" alt="" />
  <small>The vignette effect applied to several images.</small>
</div>

###jQuery Uploads

Cloudinary has a CORS API for file uploads which degrades to an `iframe` in legacy browsers.  This means you can do image uploads with no server-side code at all!  The [cloudinary_js](https://github.com/cloudinary/cloudinary_js) repository has a jQuery plugin, with jQuery UI support, which can be used to upload images.

Download the JavaScript files from [the cloudinary/cloudinary_js repository](https://github.com/cloudinary/cloudinary_js/) and add them to the `public/` folder.  Then edit `views/layout.jade` to load jQuery and the other files in this order:

{% highlight text %}
  script(src='http://ajax.googleapis.com/ajax/libs/jquery/1.9.0/jquery.min.js')
  script(src='/jquery.ui.widget.js')
  script(src='/jquery.iframe-transport.js')
  script(src='/jquery.fileupload.js')
  script(src='/jquery.cloudinary.js')
  block scripts
{% endhighlight %}

The `block scripts` part at the end is some [Jade](http://jade-lang.com/) jiggery-pokery to allow HTML to be appended to this template from another template.  Open `views/index.jade` and add this markup:

{% highlight text %}
  h2 jQuery Uploads

  .preview

  form(enctype="multipart/form-data")!=cloudinary.uploader.image_upload_tag('image')

block scripts
  script(type="text/javascript")
    // Configure Cloudinary
    $.cloudinary.config({ api_key: '!{api_key}', cloud_name: '!{cloud_name}' });

    $('.cloudinary-fileupload').bind('fileuploadstart', function(e){
      $('.preview').html('Upload started...');
    });

    // Upload finished
    $('.cloudinary-fileupload').bind('cloudinarydone', function(e, data){
      $('.preview').html(
        $.cloudinary.image(data.result.public_id, { format: data.result.format, version: data.result.version, crop: 'scale', width: 100, height: 100 })
      );
      return true;
    });
{% endhighlight %}

This displays a form with a file `input`, generated by the `cloudinary.uploader.image_upload_tag` helper.  That keeps the markup lightweight by doing all of the signing and other things Cloudinary's API needs behind the scenes.

The client-side JavaScript at the end of the template will display a message when an image is being uploaded, and then display it once it's finished uploading.  The other event which I haven't used here is `fileuploadfail`, which is, of course, useful for displaying errors when file uploads fail.

If you want to read more about Cloudinary and jQuery, check out this article: [Direct image uploads from the browser to the cloud with jQuery](http://cloudinary.com/blog/direct_image_uploads_from_the_browser_to_the_cloud_with_jquery), [Upload Images: Remote Uploads](http://cloudinary.com/documentation/upload_images#remote_upload).

###Summary

<div class="image">
  <img src="/images/posts/cloudinary-done.png" alt="" />
  <small>The completed gallery.</small>
</div>

In this tutorial you've seen how to integrate both Node and client-side projects with Cloudinary.  If you'd like more details on the service, visit [Cloudinary.com](http://cloudinary.com/).

This gallery example could be easily expanded using features from Cloudinary's API to do a lot of practical and cool stuff:

* Pagination could be added
* The effects API could be used for editing photos
* Face detection could be used to tag people in photos

The full source for my example Express app is available here: [https://github.com/alexyoung/dailyjs-cloudinary-gallery](https://github.com/alexyoung/dailyjs-cloudinary-gallery).
