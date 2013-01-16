---
layout: post
title: "Node Roundup: 0.8.17, 0.9.6, gelf-node, jsong, Stuff.js"
author: "Alex Young"
categories: 
- node
- modules
- unix
- cli
- json
- sandbox
- search
---

<div class="intro">
You can send in your Node projects for review through our <a href="/contact.html">contact form</a> or <a href="http://twitter.com/dailyjs">@dailyjs</a>.
</div>

###Node 0.8.17, 0.9.6 (Unstable)

[Node 0.8.17](http://blog.nodejs.org/2013/01/09/node-v0-8-17-stable/) was released last week with a security fix for TypedArrays, so you should upgrade if you're using them:

> If user input can affect the size parameter in a TypedArray, an integer overflow vulnerability could allow an attacker to write to areas of memory outside the intended buffer.

The unstable branch also saw a new release with [0.9.6](http://blog.nodejs.org/2013/01/11/node-v0-9-6-unstable/).  The streams API has changed slightly again as it continues to be developed: Isaac Schlueter added the `readable.push` method, and there are also fixes for TypedArrays in this branch too.

###gelf-node

I've had a lot of luck with [ElasticSearch](http://www.elasticsearch.org/).  The last time I used it was on a project that used Node HTTP crawlers to index thousands of sites, and it was all backed by ElasticSearch.  It worked extremely well and I actually got paid!  If you're also using ElasticSearch, then you might be interested in the gelf-node module (GitHub: [robertkowalski / gelf-node](https://github.com/robertkowalski/gelf-node), License: _MIT_, npm: [gelf](https://npmjs.org/package/gelf)) by Robert Kowalski.  It works with [Graylog2](http://www.graylog2.org/), allowing messages to be sent from Node:

{% highlight javascript %}
var Gelf = require('gelf');
var gelf = new Gelf({
  graylogPort: 12201,
  graylogHostname: '127.0.0.1',
  connection: 'wan',
  maxChunkSizeWan: 1420,
  maxChunkSizeLan: 8154
});

// The readme has an example message
gelf.emit('gelf.log', message);
{% endhighlight %}

Graylog2 itself is released under the GPL (version 3).

###jsong

jsong (GitHub: [textgoeshere / jsong](https://github.com/textgoeshere/jsong), npm: [jsong](https://npmjs.org/package/jsong), License: _MIT_) by Dave Nolan is a CLI tool and module for filtering JSON.  It's built with [streamin](https://npmjs.org/package/streamin) and [clarinet](https://npmjs.org/package/clarinet), and shows full paths to matches:

{% highlight text %}
$ cat my.json | jsong -k 'z\wp'

foo.bar.zip: val1
foo.bar.zap: val2
quux.zip: val
{% endhighlight %}

Because it's built using streams, it should handle large JSON files.

###Stuff.js

Here's another project by Amjad Masad from Codecademy: [Stuff.js](http://blog.amasad.me/2012/12/11/stuffjs/) (GitHub: [Codecademy / stuff.js](https://github.com/Codecademy/stuff.js), License: _MIT_) -- an easy way to run arbitrary HTML and JavaScript in an `iframe`.  It uses node-static and uglify-js to create a sandbox for securely running user-contributed code.

There's an example in [Amjad's blog post](http://blog.amasad.me/2012/12/11/stuffjs/) that shows how to use it:

{% highlight javascript %}
stuff(secureIframeUrl, function (context) {
  var html = CodeMirror.fromTextArea($('#html'), {
    onChange: reload
  , mode: 'text/html'
  });
  var js = CodeMirror.fromTextArea($('#js'), {
    onChange: reload
  , mode: 'javascript'
  });
  var css = CodeMirror.fromTextArea($('#css'), {
    onChange: reload
  , mode: 'css'
  });

  var t = null;
  function reload () {
    clearTimeout(t);
    t = setTimeout(function () {
      var code = '<!DOCTYPE html><html><head>';
      code += '<style>'  + css.getValue() + '</style>';
      code += '<body>' + html.getValue();
      code += '<script>' + js.getValue() + '</script>';
      code += '</body></html>';
      context.load(code);
    }, 50);
  }
  reload();
});
{% endhighlight %}

