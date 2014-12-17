---
layout: post
title: "Node Roundup: watch-network, MailDev, node-notifier"
author: Alex Young
image: "/images/posts/maildev.png"
categories:
- node
- modules
- libraries
- notifications
- network
- vm
- automation
- email
---

###watch-network

If you use something like Docker or Vagrant and want to listen for file notifications over the network, then watch-network (GitHub: [efacilitation/watch-network](https://github.com/efacilitation/watch-network), License: _MIT_, npm: [watch-network](https://www.npmjs.com/package/watch-network)) by Johannes Becker might come in handy.  It can be used with Gulp, so you could run Gulp tasks when a specific network notification comes in.

Here's a basic example:

{% highlight javascript %}
var watch = WatchNetWork({
  configs: [{
    patterns: 'lib/*.coffee',
    tasks: 'something:important',
    onLoad: true
  }]
});

watch.task('something:important', function(changedFiles) {
  // ..
});

watch.initialize();
{% endhighlight %}

Here's the use-case that Johannes described:

> Scenario: You use Vagrant/VirtualBox in your workflow to have services and configurations in an encapsulated environment. For developing purposes you now sync a local directory into the VM using vboxfs, nfs, rsync or similar. In your VM you want to use watcher facilities for developing-concerns, but for some reason triggering inotify over the network seems to be troublesome or unreliable.

###MailDev

![MailDev](/images/posts/maildev.png)

If you've ever felt like handling emails in web applications is messy, and you don't feel like your emails are as good as they could be, then you're not alone!  I always feel like emails are annoying to develop, so I thought [MailDev](http://djfarrelly.github.io/MailDev/) (GitHub: [mikaelbr/node-notifier](https://github.com/mikaelbr/node-notifier), License: _MIT_, npm: [maildev](https://www.npmjs.com/package/maildev)) looked interesting.  This module helps you test your project's generated emails during development with a responsive web interface.  It has a Node API, and there's even a REST API so you could integrate it with other services.

Emails are displayed with WebSockets, so you don't have to keep refreshing, and it'll show HTML, text, and attachments.

I currently send all the generated emails to a temporary directory, then open them up when I need to.  MailDev seems like a much better solution.

###node-notifier

Mikael Brevik sent in node-notifier (GitHub: [mikaelbr/node-notifier](https://github.com/mikaelbr/node-notifier), License: _MIT_, npm: [node-notifier](https://www.npmjs.com/package/node-notifier)), in response to the recent mention of [trayballoon](https://www.npmjs.com/package/trayballoon).  Node-notifier tries to smooth out the differences between each platform, so you can use notification features that are present on all platforms more easily.  It also supports actions on notifications.

Mikael notes that it works with node-webkit, which is cool if you're making Node desktop apps, and it supports the following notification systems:

* Mac: Notification Center, Growl
* Windows: Toasters, trayballoon
* Linux: notify-osd

Here's an example:

{% highlight javascript %}
var notifier = require('node-notifier');
notifier.notify({
  'title': 'My notification',
  'message': 'Hello, there!'
});
{% endhighlight %}
