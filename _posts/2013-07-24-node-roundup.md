---
layout: post
title: "Node Roundup: Magnolia, VMUX, joinr"
author: "Alex Young"
categories: 
- node
- modules
- mongodb
- video
- webrtc
---

<div class="intro">
You can send in your Node projects for review through our <a href="/contact.html">contact form</a>.
</div>

###Magnolia

Ryan Munro sent in some of his projects, including Magnolia (GitHub: [Submersible / node-magnolia](https://github.com/Submersible/node-magnolia), License: _MIT_, npm: [magnolia](https://npmjs.org/package/magnolia)) and Figs (GitHub: [Submersible / node-figs](https://github.com/Submersible/node-figs), License: _MIT_).  Magnolia is a MongoDB client library that has a chainable API and support for promises, which means you can compose expressions using a natural JavaScript-friendly syntax.

{% highlight javascript %}
magnolia('user')
  .filter({_id: ObjectID('4e4e1638c85e808431000003')})
  .one()
  .then(function(user) {
      console.log('hello', user.name);
  });
{% endhighlight %}

Figs is a module for working with settings stored in JSON files.  It supports local overrides, "parent directory clobbering", and overriding when environmental variables are set.  It also includes a command-line tool for viewing configurations.

###VMUX

![VMUX](/images/posts/vmx-logo.png)

[VMUX](http://vmux.co/) (GitHub: [malditogeek / vmux](https://github.com/malditogeek/vmux), License: _BSD_) by Mauro Pompilio is an open source video call application that works in browsers, and uses Node.  Nodejitsu wrote about it as part of their [open source project of the month](http://blog.nodejitsu.com/featured-open-source-project-vmux) programme.  The readme includes details on how to set it up locally, but you can also try out the service running on Nodejitsu by signing in with Twitter.

[Nodejitsu's blog](http://blog.nodejitsu.com/) has had a flurry of activity recently, including [a cool post about GUI console applications](http://blog.nodejitsu.com/a-blessed-ui-for-jitsu).

###joinr

There is another MongoDB module this week that I wanted to write about: joinr (GitHub: [punkave / joinr](https://github.com/punkave/joinr), License: _MIT_, npm: [joinr](https://npmjs.org/package/joinr)) by Tom Boutell.  This one fetches related documents by performing join-related operations:

> joinr allows joins to be performed via IDs stored in a regular property (byOne) or in an array property (byArray). Joins can be performed when the ID of the related document is in the document you already have (byOne or byArray) and also when the related documents contain the IDs of documents you already have (byOneReverse and byArrayReverse).

For example, a one-to-many join through an array property looks like this:

{% highlight javascript %}
joinr.byArray(users, 'groupIds', '_groups', function(ids, callback) {
  return groupsCollection.find({ groupIds: { $in: ids } }, callback);
}, callback);
{% endhighlight %}

There are more examples in the readme.
