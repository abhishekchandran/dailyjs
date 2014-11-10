---
layout: post
title: "JSON File Store, Purplecoat.js"
author: "Alex Young"
image: "/images/posts/purplecoat.png"
categories:
- json
- database
- memory
- libraries
- ui
- themes
---

###JSON File Store

I've been emailed a selection of in-memory databases, spurred on by last week's [LokiJS post](http://dailyjs.com/2014/11/04/lokijs/).  [JSON file store](https://github.com/flosse/json-file-store) (npm: [jfs](https://www.npmjs.org/package/jfs), License: _MIT_) by flosse can save JSON to files, and it also has a `pretty` option for producing readable output.

It can generate IDs using the [node-uuid](https://www.npmjs.org/package/node-uuid) module, but it also works with custom IDs as well.  It supports synchronous operations for saving and getting items.  The basic usage looks like this:

{% highlight javascript %}
var Store = require('jfs');
var db = new Store('data');

var d = {
  foo: 'bar'
};

// Save with custom ID
db.save('anId', d, function(err) {
  // Now the data is stored in the file data/anId.json
});

// Save with generated ID
db.save(d, function(err, id) {
  // id is a unique ID
});
{% endhighlight %}

You can toggle memory-only mode with the `type: 'memory'` option.  I thought this project seemed like something that might be useful if you've got configuration or small data files files that are user editable, perhaps in a redistributable web application or daemon.

###Purplecoat.js

Elle Kasai sent in [Purplecoat.js](http://ellekasai.github.io/purplecoat.js/) (GitHub: [ellekasai / purplecoat.js](https://github.com/ellekasai/purplecoat.js), License: _MIT_, Bower: _purplecoat.js_), a lightweight version of those popover tutorial libraries.  It can be applied to an element with the `data-purplecoat` attribute, and `data-purplecoat-label` can be used to add a message.

Purplecoat.js is used to document Elle's [Shiori Bootstrap theme for Jekyll](http://ellekasai.github.io/shiori/introducing-shiori/), which is a clean and minimal Jekyll theme with several built-in colour themes.
