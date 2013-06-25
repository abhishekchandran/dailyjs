---
layout: post
title: "jQuery Roundup: Backbone Associations, bootstrap-wysihtml5"
author: Alex Young
categories:
- jquery
- plugins
- bootstrap
- backbone.js
- text
- wysiwyg
---

<div class="intro">
Note: You can send your plugins and articles in for review through our <a href="http://contact.dailyjs.com/project">contact form</a>.
</div>

###Backbone Associations

[Backbone Associations](http://dhruvaray.github.io/backbone-associations/) (GitHub: [dhruvaray / backbone-associations](https://github.com/dhruvaray/backbone-associations), License: _MIT_, bower: _backbone-associations_) by Dhruva Ray is a plugin for one-to-one and one-to-many associations between models and collections:

> applications can listen to any kind of change (change, add, remove, reset, sort, destroy) in this hierarchy using standard Backbone events and respond to them. (views can re-render for example). The implementation strives to be tiny (2.2KB), easy-to-understand, light-weight and fast.

Once the plugin has been loaded, models can be defined using `Backbone.AssociatedModel`, and then relationships can be set up with `Backbone.One` and `Backbone.Many`.

{% highlight javascript %}
var Product = Backbone.AssociatedModel.extend({
});

var User = Backbone.AssociatedModel.extend({
  relations: [{
    type: Backbone.Many,
    key: 'locations',
    relatedModel: Product
  }]
});
{% endhighlight %}

The reversed association is automatically inferred, so a `product` could be set for a `user`.  Values can be traversed using fully qualified paths as well:

{% highlight javascript %}
emp.get('works_for.controls[0].locations[0].zip');
{% endhighlight %}

Fully qualified paths can also be used to assign event listeners:

{% highlight javascript %}
emp.on('change:works_for.locations[*]', cb);
{% endhighlight %}

The author has written up a full [tutorial for Backbone Associations](http://dhruvaray.github.io/backbone-associations/tutorial.html), and has included unit tests and full documentation.

###bootstrap-wysihtml5

[bootstrap-wysihtml5](http://jhollingworth.github.io/bootstrap-wysihtml5/) (GitHub: [jhollingworth / bootstrap-wysihtml5/](https://github.com/jhollingworth/bootstrap-wysihtml5/), License: _MIT_, bower: _bootstrap-wysihtml5_) by James Hollingworth is an amazing text editor component.  It's highlight consistent with Bootstrap's design, and has many features you may take for granted when editing text, like the usual keyboard shortcuts.

Trantor Liu sent in his fork, [trantorLiu/bootstrap-editor](https://github.com/trantorLiu/bootstrap-editor), which pairs up the project with jQuery-File-Upload.  This adds support for things like upload progress, drag and drop, and cross-domain uploads.  Trantor notes that the demo won't currently work because there's no server-side support, but he's provided instructions on how to set it up locally.

