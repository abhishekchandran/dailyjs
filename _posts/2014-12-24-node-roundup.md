---
layout: post
title: "Node Roundup: 0.10.35, Prettiest, Artisan Validator"
author: Alex Young
image: "/images/posts/d3reactchart-small.png"
categories:
- node
- modules
- libraries
- command-line
- validation
---

###Node 0.10.35

[Node 0.10.35 was released today](http://blog.nodejs.org/2014/12/23/node-v0-10-35-stable/), which has some changes to timers relating to the unref behaviour:

* timers: don't close interval timers when unrefd (Julien Gilli)
* timers: don't mutate unref list while iterating it (Julien Gilli)

This was released soon after [0.10.34](http://blog.nodejs.org/2014/12/17/node-v0-10-34-stable/), which updated v8, uv, zlib, and some core modules including child_process and crypto.

###Prettiest

What if you want to prevent a command-line script from executing more than once?  Prettiest (GitHub: [punkave/prettiest](https://github.com/punkave/prettiest), License: _MIT_, npm: [prettiest](https://www.npmjs.com/package/prettiest)) from P'unk Avenue LLC combines data storage and locking, and should work well for Node command-line scripts made with modules like [ShellJS](https://github.com/arturadib/shelljs).

This is the simplest example -- it will track how many times it has been run:

{% highlight javascript %}
var data = require('prettiest')();

data.count = data.count || 0;
data.count++;
console.log('I have been run', data.count, ' times.');
{% endhighlight %}

I've often wanted to persist data in command-line scripts, but didn't want to bother with sqlite or JSON file serialisation, so this seems ideal for such cases.  And even if you want the locking behaviour, your scripts can still be asynchronous.

###Artisan Validator

Connor Peet is on a quest to create a simple and well-documented data validator for Node.  Artisan Validator (GitHub: [MCProHosting/artisan-validator](https://github.com/MCProHosting/artisan-validator), License: _MIT_, npm: [artisan-validator](https://www.npmjs.com/package/artisan-validator)) allows you to define rules that get validated against objects, so you can easily hook it into a Node web application:

{% highlight javascript %}
var validator = require('artisan-validator')();
var rules = {
  username: ['required', 'between: 4, 30', 'alphanumeric'],
  password: ['required', 'longer: 5'],
  acceptTOS: ['required', 'boolean: true']
};

validator.try(req.body, rules).then(function (result) {
  if (result.failed) {
    res.json(400, result.errors);
  } else {
    registerAccount();
  }
});
{% endhighlight %}

You can add custom validators with `validator.validators.add`, but there are quite a few built-in rules that cover JavaScript types, and various string and date formats.  The error messages can be localised as well.

