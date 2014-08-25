---
layout: post
title: "Ment.io, Coffea, Marilyn"
author: "Alex Young"
categories:
- libraries
- ui
- WebSocket
- angularjs
---

###Ment.io

![Ment.io](/images/posts/mentio.png)

[Ment.io](http://jeff-collins.github.io/ment.io/) (GitHub: [jeff-collins / ment.io](https://github.com/jeff-collins/ment.io), License: _MIT_) is a UI component for handling Twitter/GitHub style `@` mentions.  It has no dependency on jQuery, and it's designed for use with AngularJS.

An `ngModel` is used for data, and the `mentio-menu` element is used to define the menu that appears during typing.  You can use the `mentio` on a suitable `input` or content editable element to indicate where Mentio should appear.

###Coffea

Coffea (GitHub: [caffeinery / coffea](https://github.com/caffeinery/coffea), License: _BSD_, [coffea](https://www.npmjs.org/package/coffea)) by Daniel Bugl is an event-based IRC client library.  It supports SSL, and the API seems very friendly to Node developers:

{% highlight javascript %}
var client = require('coffea')({
  host: 'irc.freenode.org'
});

client.on('motd', function(motd) {
  client.join(['#foo', '#bar', '#baz']);
});

client.on('message', function(event) {
  console.log('[' + event.channel.getName() + '] ' + event.user.getNick() + ': ' + event.message);
});
{% endhighlight %}

###Marilyn

Marilyn (GitHub: [alanjames1987 / marilyn](https://github.com/alanjames1987/marilyn), License: _MIT_) by Alan James Pub/Sub model API with a similar API to Mongoose.  It's event-based, so you can hook into events that are triggered before and after CRUD operations.

You can create models like this:

{% highlight javascript %}
var MyModel = Marilyn.model('someModelName');
{% endhighlight %}

The before and after events can be defined in the initialisation callback that gets passed to the model method.

{% highlight javascript %}
Marilyn.model('someModelName', function() {
  this.before('create', function(data, next) {
    // this is useful for validating data before a CRUD method runs
    console.log('I ran before');
    next();
  });

  this.after('create', function(data, next) {
    // this is useful for altering data before it's returned to the controller
    console.log('I ran after');
    next();
  });
});
{% endhighlight %}


