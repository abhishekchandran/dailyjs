---
layout: post
title: "Node Roundup: thin-orm, node-tar.gz, connect-bruteforce"
author: "Alex Young"
categories: 
- node
- modules
- middleware
- express
- compression
- databases
---

<div class="intro">
You can send in your Node projects for review through our <a href="/contact.html">contact form</a> or <a href="http://twitter.com/dailyjs">@dailyjs</a>.
</div>

###thin-orm

[thin-orm](https://github.com/on-point/thin-orm) (License: _MIT_, npm: [thin-orm](https://npmjs.org/package/thin-orm)) by Steve Hurlbut is a lightweight ORM module for SQL databases with a MongoDB-inspired API:

{% highlight javascript %}
var orm = require('thin-orm');

orm.table('users')
   .columns('id', 'login', 'firstName', 'lastName', 'createdAt');
{% endhighlight %}

It's designed to be used with existing libraries, like [pg](https://npmjs.org/package/pg) and [sqlite3](https://npmjs.org/package/sqlite3), so you'll need one of those modules installed to use it.

thin-orm currently supports the following features:

* Filtering
* Sorting
* Pagination
* Joins
* Optional camelCase property-to-field mapping
* SQL injection protection

Steve has included Nodeunit tests that cover the basic functionality, and some integration tests for PostgreSQL and SQLite.

###node-tar.gz

[node-tar.gz](https://github.com/cranic/node-tar.gz) (License: _MIT_, npm: [tar.gz](https://npmjs.org/package/tar.gz)) by Alan Hoffmeister is a `tar` helper module and command-line utility, built with Node's zlib module, [tar](https://npmjs.org/package/tar), and [commander](https://npmjs.org/package/commander).

The module can be used to easily tar and compress a folder, and it will install a `targz` script that supports the `zxvf` flags.  There are also Vows tests.

###connect-bruteforce

[connect-bruteforce](https://github.com/revington/connect-bruteforce) (License: _GPLv2_, npm: [connect-bruteforce](https://npmjs.org/package/connect-bruteforce)) by Pedro Narciso García Revington provides middleware that can help prevent bruteforce attacks.  It will add a small delay to requests when an attack is detected.

The author has written a useful example that requires captcha validation after a successive number of validation failures: [express-recaptcha](https://github.com/revington/connect-bruteforce/tree/master/examples/express-recaptcha).

For a simpler example, see [express-hello-world](https://github.com/revington/connect-bruteforce/tree/master/examples/express-hello-world).

The project includes Mocha tests.
