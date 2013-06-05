---
layout: post
title: "Node Roundup: 0.8.24, 0.10.10, speakingurl, node-xmljson"
author: "Alex Young"
categories: 
- node
- modules
- web
- urls
- xml
- json
---

<div class="intro">
You can send in your Node projects for review through our <a href="/contact.html">contact form</a>.
</div>

###Node 0.8.24 and 0.10.10

[Node 0.8.24](http://blog.nodejs.org/2013/06/04/node-v0-8-24-maintenance/) and [Node 0.10.10](http://blog.nodejs.org/2013/06/04/node-v0-10-10-stable/) have been released.  The 0.8 (maintenance) release gets an updated npm, and some fixes for the url and http core modules.

Meanwhile, 0.10.10 has a new version of the internal uv library, and `unshift('')` now behaves like a noop.

###speakingurl

Sascha Droste sent in speakingurl (GitHub: [pid / speakingurl](https://github.com/pid/speakingurl), License: _BSD_, npm: [speakingurl](https://npmjs.org/package/speakingurl)), a module for generating clean URL slugs:

{% highlight javascript %}
slug = getSlug('Apple & Pear!');
console.log(slug);
// Output: apple-and-pear

slug = getSlug('Foo ♥ Bar');
console.log(slug);
// Output: foo-love-bar
{% endhighlight %}

It has tests, localisation support, and works in browsers.

###node-xmljson

node-xmljson (GitHub: [ExactTarget / node-xmljson](https://github.com/ExactTarget/node-xmljson), License: _MIT_, npm: [xmljson](https://npmjs.org/package/xmljson)) from Adam Alexander and Benjamin Dean of ExactTarget was just released, providing quick and simple bi-directional translation between XML and JSON formats.

#####XML to JSON:

{% highlight javascript %}
// Load the module
var to_json = require('xmljson').to_json;

// An XML string
var xml = '' +
    '<data>' +
        '<prop1>val1</prop1>' +
        '<prop2>val2</prop2>' +
        '<prop3>val3</prop3>' +
    '</data>';

to_json(xml, function (error, data) {
    // Module returns a JS object
    console.log(data);
    // -> { prop1: 'val1', prop2: 'val2', prop3: 'val3' }

    // Format as a JSON string
    console.log(JSON.stringify(data));
    // -> {"prop1":"val1","prop2":"val2","prop3":"val3"}
});
{% endhighlight %}

#####JSON to XML:

{% highlight javascript %}
// Load the module
var to_xml = require('xmljson').to_xml;

// A JSON string
var json = '' +
    '{' +
        '"prop1":"val1",' +
        '"prop2":"val2",' +
        '"prop3":"val3"' +
    '}';

to_xml(json, function (error, xml) {
    // Module returns an XML string
    console.log(xml);
    // -> <data><prop1>val1</prop1><prop2>val2</prop2><prop3>val3</prop3></data>
});
{% endhighlight %}

ExactTarget has also released [Fuel UX](http://exacttarget.github.io/fuelux) (GitHub: [ExactTarget / fuelux](https://github.com/ExactTarget/fuelux), License: _MIT_) a lightweight web UI library that extends Twitter Bootstrap with additional JavaScript controls.

