---
layout: post
title: "Node Roundup: Conductance, Easymongo, Schema-Inspector"
author: Alex Young
categories:
- node
- modules
- frameworks
- mongodb
- schema
---

###Conductance

![Conductance](/images/posts/conductance.png)

[Conductance](https://conductance.io/) (GitHub: [onilabs / conductance](https://github.com/onilabs/conductance), License: _GPL_, npm: [conductance](https://npmjs.org/package/conductance)) from Oni Labs is a web application server with a UI toolkit and a module system that's compatible with client-side code.

It's built on [Stratified JavaScript](http://onilabs.com/stratifiedjs), by the same company, which adds new language primitives for block lambdas, destructuring data, arrow function syntax, and more.

[Conductance already has a detailed tutorial](https://conductance.io/examples/chat/), and there's [an API guide](https://conductance.io/reference) as well.

###Easymongo

[Easymongo](http://meritt.github.io/easymongo/) (GitHub: [meritt / easymongo](https://github.com/meritt/easymongo), License: _MIT_, npm: [easymongo](https://npmjs.org/package/easymongo)) by Alexey Simonenko is a wrapper around the native Node MongoDB driver.  It has a clean, idiomatic API, and relies on plain old objects instead of models.

It has Mocha tests, and the API is documented in the readme.  Basic use looks like this:

{% highlight javascript %}
var options = {
  dbname: 'test'
};

var mongo = new require('easymongo')(options);
var users = mongo.collection('users');

var data = { name: 'Alexey', surname: 'Simonenko', url: 'http://simonenko.su' };
users.save(data, function(error, results) {
  // Returns a new document (array).
  console.log(results);
});

users.find({ name: 'Alexey' }, { limit: 1 }, function(error, results) {
  // Always return array of documents.
  console.log(results);
});
{% endhighlight %}

###Schema-Inspector

What do you do when you're using simple objects without an ORM layer?  You use schemas to validate your user input!  [Schema-Inspector](http://atinux.github.io/schema-inspector/) (GitHub: [Atinux / schema-inspector](https://github.com/Atinux/schema-inspector), License: _MIT_, npm: [schema-inspector](https://npmjs.org/package/schema-inspector), Bower: _schema-inspector_) by Sebastien Chopin is a JavaScript object validator that works in browsers and Node.

Given a suitable schema, you can validate objects like this: `inspector.validate(schema, candidate)`.  It can also be called asynchronously, which allows you to report issues with `this.report` inside functions in the schema.

It has tests written with Mocha, and a healthy amount of API documentation in the readme.
