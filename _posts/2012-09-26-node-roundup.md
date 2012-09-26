---
layout: post
title: "Node Roundup: 0.8.10-11, Cabinet, Node Si"
author: "Alex Young"
categories:
- node
- modules
---

<div class="intro">
You can send in your Node projects for review through our <a href="/contact.html">contact form</a> or <a href="http://twitter.com/dailyjs">@dailyjs</a>.
</div>

###0.8.10

Node 0.8 releases are still coming thick and fast, with the release of [0.8.10](http://blog.nodejs.org/2012/09/25/node-v0-8-10-stable/) this week.  On average the 0.8 branch has seen approximately 9 days between releases, with an extended summer holiday period of 20 days in August and September.

This version has a few `fs` fixes by Ben Noordhuis, although he's already cited an [issue in fs.stat()](https://groups.google.com/d/msg/nodejs/udqSi9liP2o/t2kUFB73OukJ) so he's recommending holding off for 0.8.11 which should be released later this week.

###Cabinet

[Cabinet](OptimalBits/cabinet) (License: _MIT_, npm: [cabinet](https://npmjs.org/package/cabinet)) by Manuel Astudillo is an alternative to [Connect's static middleware](http://extjs.github.com/Connect/staticProvider.html).  The changes from TJ's original module are as follows:

* Memory-based cache, based on [fs.watch](http://nodejs.org/docs/latest/api/all.html#all_fs_watch_filename_options_listener)
* Automatic asset compilation and minification
* gzip
* Support for "virtual" files, including cache manifests

The API is compatible with Connect and Express middleware, but there are additional options:

{% highlight javascript %}
app.use(cabinet(__dirname + '/static', {
  coffee: true,
  gzip: true,

  less: {
    // Specify search paths for @import directives
    paths: ['.',__dirname + '/static/stylesheets']
  },

  cache: { maxSize: 1024, maxObjects:256 }
}));
{% endhighlight %}

The project comes with Mocha tests, and additional options are documented in the readme file.

###Node Si

[Node Si](https://github.com/MichalCz/node-si) (License: _MIT_, npm: [si](https://npmjs.org/package/si)) by Michał Czapracki is a binary prefix number parser and formatter module.  It can be used to format numbers like `10000000` as `10M`, or `10gb` as `1e10`.

It's currently a simple module, but the author plans on adding IEC compliant binary multipliers like 'MiB', case sensitive formats, and fractional SI multipliers.
