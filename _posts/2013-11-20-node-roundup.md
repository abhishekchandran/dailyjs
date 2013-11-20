---
layout: post
title: "Node Roundup: Fowl, grunt-ec2, connect-body-rewrite"
author: "Alex Young"
categories: 
- node
- modules
- grunt
- amazon
- foundationdb
- express
---

###Fowl

Fowl (GitHub: [OptimalBits / fowl](https://github.com/OptimalBits/fowl), License: _MIT_, npm: [fowl](https://npmjs.org/package/fowl)) by Manuel Astudillo is a document and query layer for [FoundationDB](https://foundationdb.com/).  It provides a similar API to NoSQL databases like MongoDB, but has support for multidocument transactions:

> Transaction support is an incredibly powerful feature that simplifies server logic and helps avoiding difficult to solve race conditions.

> Fowl provides a low level API based on keypaths for describing documents and its properties following CRUD semantics.

It includes tests and each API method is documented in the readme file.  Basic usage looks like this:

{% highlight javascript %}
// Open a foundationDB database
fowl.open();

// Create a document (if _id not specify a GUID will be generated)
var john = fowl.create('people', {
  _id: 'john',
  name: 'John',
  lastname: 'Smith',
  balance: 100
});

// Use transactions to transfer money from one account to another
var tr = fowl.transaction()

tr.get(['people', 'john', 'balance']).then(function(johnBalance) {
  tr.put(['people', 'john', 'balance'], johnBalance - 10);
});
{% endhighlight %}

###grunt-ec2

grunt-ec2 (GitHub: [bevacqua / grunt-ec2](https://github.com/bevacqua/grunt-ec2), License: _MIT_, npm: [grunt-ec2](https://npmjs.org/package/grunt-ec2)) by Nicolas Bevacqua is a set of Grunt tasks for creating, terminating, and deploying Node applications to AWS EC2 instances.

The deployed Node applications are served from behind an Nginx proxy.  The [task reference](https://github.com/bevacqua/grunt-ec2#complete-task-reference) explains what each task does -- there are quite a few.

It supports most of the things you want to do when setting up Node applications, including SSL, SSH keys for each instance, rsync support for fast and painless uploads, and hot code swaps.

###connect-body-rewrite

There are times when the logic of my Node web applications have seemed to need the response body to be rewritten, but in the middleware rather than the main route logic.  The connect-body-rewrite (GitHub: [rubenv / connect-body-rewrite](https://github.com/rubenv/connect-body-rewrite), License: _MIT_, npm: [connect-body-rewrite](https://npmjs.org/package/connect-body-rewrite)) by Ruben Vermeersch makes this possible.  The examples use regular expressions to replace text, based on the request headers:

{% highlight javascript %}
app.use(require('connect-body-rewrite')({
  accept: function (res) {
    return res.getHeader('content-type').match(/text\/html/);
  },
  rewrite: function (body) {
    return body.replace(/<\/body>/, "Copyright 2013 </body>");
  }
}));
{% endhighlight %}

I like the way it's designed to use an `accept` callback, because it makes it easy to see what the rewriter actually does by keeping the logic close together.
