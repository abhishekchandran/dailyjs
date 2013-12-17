---
layout: post
title: "Dynatable, nanoGallery, jQuery Audit"
author: "Alex Young"
categories: 
- jquery
- tables
- ui
- galleries
- chrome
---

###Dynatable

![Dynatable](/images/posts/dynatable.png)

[Dynatable](http://www.dynatable.com/) (GitHub: [JangoSteve / jquery-dynatable](https://github.com/JangoSteve/jquery-dynatable/), License: _AGPL or commercial_) by Steve Schwartz is a library for displaying JSON data as friendly and efficient HTML tables.  It provides a framework for searching, sorting, and filtering data.  It uses jQuery, and can be invoked with `$.dynatableSetup`.

Dynatable can convert plain HTML tables into JSON.  The properties for the JSON can be camelCase, but other styles are supported, including dashed and underscore.  This is set with the `table.defaultColumnIdStyle` option.

JSON can also be fetched from a server.  In this case you can use the `dataset` option:

{% highlight javascript %}
$('#my-ajax-table').dynatable({
  dataset: {
    ajax: true,
    ajaxUrl: '/dynatable-ajax.json',
    ajaxOnLoad: true,
    records: []
  }
});
{% endhighlight %}

It expects a corresponding skeleton `table` node, with `thead` and `tbody`.

The documentation is thorough and includes examples for each of these things, and the other features provided by the library.

###nanoGallery

Nobody's sent me a jQuery gallery for a while. nanoGALLERY (GitHub: [Kris-B / nanoGALLERY](https://github.com/Kris-B/nanoGALLERY), License: _CC BY-NC 3.0_) by Christophe Brisbois supports Flickr and Google+, and supports responsive layouts.  You can get a gallery going with a Google account like this:

{% highlight javascript %}
$('#elt').nanoGallery({
  kind: 'picasa',
  userID: 'you@example.com'
});
{% endhighlight %}

It comes with CSS, but you can theme it.  It displays a gallery navigator using folders, so it could scale up quite well to a large collection.

Documentation for the main options and expected markup can be found in the project's readme file.

###jQuery Audit

[jQuery Audit](https://chrome.google.com/webstore/detail/jquery-audit/dhhnpbajdcgdmbbcoakfhmfgmemlncjg/) (GitHub: [zertosh / jquery-audit](https://github.com/zertosh/jquery-audit), License: _MIT_) by Andres Suarez is a Chrome Developer Tools extension for auditing jQuery.  It adds a sidebar (under Elements) that includes details of delegated events and internal data.

The documentation has explanations of the main features, and instructions on how to use the extension properly.  For example, you can dig into bound functions for event handlers which can be bound differently based on the library.
