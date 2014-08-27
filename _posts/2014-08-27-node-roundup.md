---
layout: post
title: "Node Roundup: Tint, Redbird"
author: "Alex Young"
categories:
- node
- modules
- mac
- native
- http
- proxy
---

###Tint

![Tint2](/images/posts/tint2.png)

Desktop apps built with [node-webkit](https://github.com/rogerwang/node-webkit) or similar technologies are on the rise.  The idea is seemingly simple: package the Node runtime along with a small program that runs your Node web app as if it's a native application.

[Tint](https://github.com/trueinteractions/tint2) is an alternative.  It uses a modified version of Node that bridges to native components, so you can actually write JavaScript that creates native Mac windows, buttons, web views, dialogs, and more.

It's created by a company called [True Interactions](https://www.trueinteractions.com/), and is MIT licensed.  If you're an Objective-C developer you might like to check out [Main_mac.mm](https://github.com/trueinteractions/tint2/blob/master/modules/Runtime/Main_mac.mm), because this is where the authors have successfully integrated Objective-C++ with Node's event loop.

I built it from source and created a quick test application this afternoon to see what the API feels like:

{% highlight javascript %}
require('Application');

var Window = require('Window');
var Button = require('Button');

var mainWindow = new Window();
var button = new Button();

mainWindow.title = 'DailyJS';

button.title = 'Hello';
button.addEventListener('mousedown', function() {
  button.title = '^_^';
});

button.addEventListener('mouseup', function() {
  button.title = 'Hello';
});

mainWindow.appendChild(button);

mainWindow.addLayoutConstraint({
  priority: 'required',
  relationship: '=',
  firstItem: button,
  firstAttribute: 'top',
  secondItem: mainWindow,
  secondAttribute: 'bottom',
  multiplier: 0.0,
  constant: 0.0
});

setInterval(function() {
  button.title = Math.random();
}, 1000);
{% endhighlight %}

I ran the script with `./build/Release/tint example.js` and got a window with a button.  I wrote this script by looking at the [tests](https://github.com/trueinteractions/tint2/tree/master/test) to see how the API works.

I think this is a cool project and I'd really like to make a real Mac application with it, but I'm not sure how to actually distribute an application bundle that people can easily install.  I'll keep playing with it and write a longer tutorial if I discover anything.

###Redbird

Redbird (GitHub: [OptimalBits / redbird](https://github.com/OptimalBits/redbird), License: _BSD_, npm: [redbird](https://www.npmjs.org/package/redbird)) by OptimalBits is a reverse proxy for dealing with dynamic virtual hosts, load balancing, proxying web sockets and SSL encryption.

{% highlight javascript %}
var proxy = require('redbird')({port: 80});

// Route to any global ip
proxy.register('optimalbits.com', 'http://167.23.42.67:8000');

// Route to any local ip, for example from docker containers.
proxy.register('example.com', 'http://172.17.42.1:8001');
{% endhighlight %}

The documentation includes a full SSL example, and the authors are planning support for load balancing and IP filtering.
