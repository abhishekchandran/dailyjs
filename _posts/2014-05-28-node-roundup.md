---
layout: post
title: "Node Roundup: mongo-select, asynctrace"
author: "Alex Young"
categories:
- node
- modules
- npm
- testing
- mongodb
---

###mongo-select

mongo-select (GitHub: [dschenkelman / mongo-select](https://github.com/dschenkelman/mongo-select), License: _MIT_, npm: [mongo-select](https://www.npmjs.org/package/mongo-select)) is a module for creating projections on results from [mongodb](https://www.npmjs.org/package/mongodb).

You can specify the fields to include using `select.include`:

{% highlight javascript %}
var select = require('mongo-select').select();
var projection = select.include(['name', 'email', 'children.name']).make();

console.log(projection); // { 'name': false, 'email': false, 'children.name': false };
{% endhighlight %}

There are also methods for excluding fields (`exclude`) and ignoring the `_id` field (`noId`).  These methods can be chained:

{% highlight javascript %}
select.noId()._exclude(['name', 'email', 'children.name']);
{% endhighlight %}

Using it with MongoDB queries looks like this:

{% highlight javascript %}
var select = require('mongo-select').select();
var mongodb = require('mongodb');

var MongoClient = mongodb.MongoClient;

MongoClient.connect('mongodb://127.0.0.1:27017/test', function(err, db) {
  if (err) throw err;

  var users = db.collection('users');

  users.find(
    {},
    select.include(['name', 'email']),
    function(err, result) {
      // code here, access to only result[i]._id, result[i].name and result[i].email
    }
  );
});
{% endhighlight %}

###asynctrace

asynctrace (GitHub: [Empeeric / asynctrace](https://github.com/Empeeric/asynctrace), License: _MIT_, npm: [asynctrace](https://www.npmjs.org/package/asynctrace)) from Empeeric is a stack trace API based on AsyncListener.  By requiring `asynctrace`, you'll get stack traces that include details on asynchronous boundaries.

It's built using the [shimmer](https://www.npmjs.org/package/shimmer) module, which is meant to help safely replace functions by wrapping them.

If you use Mocha then you can optionally use it by specifying it on the command line: `mocha --require asynctrace`.  That means you don't need to modify your code to use the module during testing.
