---
layout: post
title: "Node Roundup: 0.10.7, JSON Editor, puid, node-mac"
author: "Alex Young"
categories: 
- node
- modules
- mac
- windows
- json
- uuid
---

<div class="intro">
You can send in your Node projects for review through our <a href="/contact.html">contact form</a>.
</div>

###Node 0.10.7

[Node 0.10.7](http://blog.nodejs.org/2013/05/17/node-v0-10-7-stable/) was released last week.  This version includes fixes for the buffer and crypto modules, and timers.  The buffer/crypto fix relates to encoding issues that could crash Node: [#5482](https://github.com/joyent/node/issues/5482).

###JSON Editor Online

![JSON Editor Online](/images/posts/jsoneditoronline.png)

[JSON Editor Online](http://jsoneditoronline.org/) (GitHub: [josdejong / jsoneditor](https://github.com/josdejong/jsoneditor/), License: _Apache 2.0_, npm: [jsoneditor](https://npmjs.org/package/jsoneditor), bower: _jsoneditor_) by Jos de Jong is a web-based JSON editor.  It uses Node for building the project, but it's actually 100% web-based.  It uses the [Ace](http://ace.ajax.org/#nav=about) editor, and includes features for searching and sorting JSON.

It's installable with Bower, so you could technically use it as a component and embed it into another project.

###english-time

Azer Koçulu sent in a bunch of new modules again, and one I picked out this time was english-time (GitHub: [azer / english-time](https://github.com/azer/english-time), License: _BSD_, npm: [english-time](https://npmjs.org/package/english-time)).  He's using it with some of the CLI tools he's written, so rather than specifying a date in an ISO format users can express durations in English.

The module currently supports milliseconds, seconds, minutes, hours, days, weeks, and shortened expressions based on combinations of these.  For example, `3 weeks, 5d 6h` would work.

###puid

puid (GitHub: [pid / puid](https://github.com/pid/puid), License: _MIT_, npm: [puid](https://npmjs.org/package/puid)) by Sascha Droste can generate unique IDs suitable for use in a distributed system.  The IDs are based on time, machine, and process, and can be 24, 14, or 12 characters long.

Each ID is comprised of an encoded timestamp, machine ID, process ID, and a counter.  The counter is based on nanoseconds, and the machine ID is based on the network interface ID or the machine's hostname.

###node-mac

[node-windows](https://github.com/coreybutler/node-windows) provides integration for Windows-specific services, like creating daemons and writing to `eventlog`.  The creator of node-windows, Corey Butler, has also released [node-mac](http://coreybutler.github.io/node-mac/manual/) (GitHub: [coreybutler / node-mac](https://github.com/coreybutler/node-mac), License: _MIT_, npm: [node-mac](https://npmjs.org/package/node-mac)).  This supports Mac-friendly daemonisation and logging.

Services can be created using an event-based API:

{% highlight javascript %}
var Service = require('node-mac').Service;

// Create a new service object
var svc = new Service({
  name: 'Hello World',
  description: 'The nodejs.org example web server.',
  script: '/path/to/helloworld.js')
});

// Listen for the "install" event, which indicates the
// process is available as a service.
svc.on('install', function() {
  svc.start();
});

svc.install();
{% endhighlight %}

It also supports service removal, and event logging.
