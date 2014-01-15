---
layout: post
title: "Node Roundup: TJ Fontaine Takes Over, Conductance, Easymongo, Schema-Inspector"
author: Alex Young
categories:
- node
- modules
- frameworks
- mongodb
- schema
---

###The Next Phase of Node.js

In [The Next Phase of Node.js](http://blog.nodejs.org/2014/01/15/the-next-phase-of-node-js/index.html), Isaac Z. Schlueter has announced that TJ Fontaine is now the Node project lead:

> Anyone who's been close to the core project knows that he's been effectively leading the project for a while now, so we're making it official. Effective immediately, TJ Fontaine is the Node.js project lead. I will remain a Node core committer, and expect to continue to contribute to the project in that role. My primary focus, however, will be npm.

Isaac also said he's founding npm, Inc., to allow him to focus on npm and develop related products:

>  I'll be sharing many more details soon about exactly how this is going to work, and what we'll be offering. For now, suffice it to say that everything currently free will remain free, and everything currently flaky will get less flaky. Pursuing new revenue is how we can keep providing the npm registry service in a long-term sustainable way, and it has to be done very carefully so that we don't damage what we've all built together.

Recently, there was an initiative by Nodejitsu to drive support and funding for npm, [resulting in over $300,000](https://npm.nodejitsu.com/) being raised.  It'll be interesting to see how this all ties together over the next year.

Congratulations and good luck to TJ Fontaine!

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
