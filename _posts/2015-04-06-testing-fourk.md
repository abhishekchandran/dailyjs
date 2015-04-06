---
layout: post
title: "Selenium and Node.js, fourk.js"
author: Alex Young
categories:
- node
- libraries
- modules
- testing
---

###Using Selenium and Node.js for Testing

David Posin sent in an article about [using a Node server to control the Selenium process](http://randomjavascript.blogspot.co.uk/2015/04/look-no-hands-using-selenium-and-nodejs.html), so the test runner is interactive:

> It occurred to me I could help alleviate this by having the browsers at the ready and eagerly waiting for the command to start testing.
>
>  I type a command into the console of my running Node server, and it instructs the already open browsers to run the tests. I like this approach because I can build my tests a little bit at a time and confirm they are working as I go. This is all possible because of the web driver component, which includes a JavaScript API, created by the Selenium team.

The script is included in the post. It works by using Node's `child_process` module to spawn a script with the Selenium browser session ID.

I've noticed a lot of people struggle to get solid and reliable full-stack tests working, so if you've been looking for a better Selenium workflow then this might help.

###fourk.js

fourk.js (GitHub: [crcn/fourk.js](https://github.com/crcn/fourk.js), License: _MIT_, npm: [fourk](https://www.npmjs.com/package/fourk)) by Craig Condon has an API that's like [clusterjs](https://www.npmjs.com/package/clusterjs) but for forking web workers in a browser:

{% highlight javascript %}
var cluster = require('fourk');

if (cluster.isMaster) {
  for (var i = 4; i--;) cluster.fork()
} else {
  // do stuff as worker
}
{% endhighlight %}

The `cluster` object uses `EventEmitter`, so you can `emit` messages to workers, and listen with `on` or `once`.  This will definitely appeal to Browserify front-end developers who want web workers.
