---
layout: post
title: "Node Roundup: pkgcloud, rewire, ssh2"
author: "Alex Young"
categories: 
- node
- modules
- ssh
- cloud
- testing
---

<div class="intro">
You can send in your Node projects for review through our <a href="/contact.html">contact form</a> or <a href="http://twitter.com/dailyjs">@dailyjs</a>.
</div>

###pkgcloud

[pkgcloud](http://blog.nodejitsu.com/introducing-pkgcloud) (GitHub: [nodejitsu / pkgcloud](https://github.com/nodejitsu/pkgcloud), License: _MIT_, npm: [pkgcloud](https://npmjs.org/package/pkgcloud)) from Nodejitsu is a module for scripting interactions with cloud service providers.  It supports various services from Joyent, Microsoft, Rackspace, and several database providers like MongoHQ and RedisToGo.  The authors have attempted to unify the vocabulary used by each provider -- for example, pkgcloud uses the term 'Server' to refer to Joyent's "machines" and Amazon's "instances".

Services can be introspected and resources can be fetched.  The API is naturally asynchronous, with callback arguments using the standard error-first pattern.

The roadmap promises support for more services in the future, including CDN and DNS.

###rewire

[rewire](https://github.com/jhnns/rewire) (License: _MIT_, npm: [rewire](https://npmjs.org/package/rewire) by Johannes Ewald is a [dependency injection](http://en.wikipedia.org/wiki/Dependency_injection) implementation that can be used to inject mocks into other modules and access private variables.

As an example, consider a module within your project that uses the standard `fs` module to read a file.  When writing tests for this module, it would be entirely possible to use rewire to modify the `fs` module to mock the `readFile` method:

{% highlight javascript %}
var rewire = require('rewire')
  , exampleModule = rewire('./exampleModule')
  ;

exampleModule.__set__('fs', {
  readFile: function(path, encoding, cb) {
    cb(null, 'Success!');
  }
});

// Tests would follow...
{% endhighlight %}

Notice that `rewire` was used instead of `require` -- rewire itself works by appending special getters and setters to modules rather than using an `eval`-based solution.

###SSH2

[SSH2](https://github.com/mscdex/ssh2) (License: _MIT_, npm: [ssh2](https://npmjs.org/package/ssh2)) by Brian White is an SSH2 client written in pure JavaScript.  It's built with the standard Node modules -- streams, buffers, events, and lots of prototype objects and regular expressions.

It supports several authentication methods, including keys, bidirectional port forwarding, execution of remote commands, interactive sessions, and SFTP.  Brian has provided some detailed examples of how to use the library's event-based API.
