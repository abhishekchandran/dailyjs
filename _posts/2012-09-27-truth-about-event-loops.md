---
layout: post
title: "The Truth About Event Loops"
author: Alex Young
categories:
- node
- tutorials
- sponsored-content
---

<div class="sponsored-content">
  <p><a class="label" href="/sponsored-content.html">Sponsored Content</a> This post is about a commercial product that we think will appeal to DailyJS readers.</p>
</div>

![The Truth About Event Loops](/images/posts/thetruthaboutevents.png)

[The Truth About Event Loops](http://truthabouteventloops.com/) is an online masterclass by [Marc-André Cournoyer](http://truthabouteventloops.com/), the creator of the [Thin](http://code.macournoyer.com/thin/) web server used by Apple, CloudFoundry, and Heroku.  Each class is limited to 25 people, and includes eight hours of content, downloadable recordings, cheatsheets, exercises, reusable source code, and a copy of [Create Your Programming Language](http://createyourproglang.com/).  The class is priced at $529 CAD, but there are early bird tickets for $479 CAD which is around $488 USD.

Classes last for two days, and the next will be held on October 23rd and 24th at 9AM-1PM ET -- keep in mind the time zone if you're booking from outside Canada!

By taking part in this class, you'll learn the following:

* Guidelines for evented I/O
* Why and when asynchronous I/O is faster
* How an event loop works, by building one from scratch
* The system calls at the core of every server
* How to write the fastest network applications around
* Ways to use your machine's resources to the maximum

The aim is to allow you to finally master your web stack from top to bottom!

To give us a taste of the class, Marc has written a tutorial all about the Node event loop.

###The Heart of the Node Event Loop

I am a big believer in mastering your tools to become a better developer. And the best way to master your tools is to understand how they are made.

Do you know what's happening inside Node?

There's an event loop. So there must be a loop somewhere, right? A loop handling events. Let's take a look...

###The Loop

Event loops like the one in Node are designed to react to I/O events.  This could be an incoming connection, data arriving on a socket, etc.  What's more, it must react to these events extremely quickly. Like most things in software, the simplest design is usually the fastest. And event loops are usually very simple.

First, it consists of an endless loop:

{% highlight javascript %}
while (true) {
  ...
}
{% endhighlight %}

Everything will happen in that loop. All of your Node programs will be running inside that loop. Which is similar to the loop you'll find in virtual machines and emulators, where an actual processor is simulated instead.

###A Turn in the Loop

Somewhere in the loop, your process will wait for I/O events to happen. Luckily, most operating systems come with a function that allows us to do just that. Several options exist, such as `kqueue` on Mac OS, `epoll` on Linux. The most portable (but slowest) one is `select`. For more on this, see [select (2)](http://www.kernel.org/doc/man-pages/online/pages/man2/select.2.html).

`select` watches a bunch of I/O objects (files, sockets) and lets you know when something happens. It looks something like this:

{% highlight text %}
while (true) { // That's our loop
  events = select(<I/O objects to watch>)
}
{% endhighlight %}

###React

At this point in the loop, we know an event has occurred. We must react to those events. In Node and many other event-based systems, this is done via callbacks.

In your Node program, you'll define callbacks like so:

{% highlight javascript %}
object.on('read', function() { ... })
{% endhighlight %}

This will register the callback inside the event loop, so that it knows what to do when this event happens. Introducing that in our loop, we'll end up with the following:

{% highlight text %}
while (true) {
  var events = select(<I/O objects to watch>)
  
  events.forEach(function(event) {
    var callback = findCallbackForEvent(event)
    callback() // This calls the callback function
  });
}
{% endhighlight %}

After we're done executing all of the callbacks, we're ready for another turn in the loop -- it'll patiently wait for other I/O events to happen.

###But There's More!

This is a simplification of how things work internally. However, even if the Node event loop is a little more complex than that, the structure is the same. It's still a loop using `select` (or a variation), and triggering callbacks.

If you'd like to dive deeper into event loops and how it works in Node, and how other features such as `setTimeout` are implemented, then [join the next edition of my online class](http://truthabouteventloops.com/).

Everything is online. You can ask questions. You'll get exercises. And you'll also get recordings of the class to watch again at your leisure.

The class already helped a number of developers master Node. Here's what one of them had to say:

> The class was paced excellently. Overall, this subject matter is complicated — but Marc walks through the material step-by-step and it's straightforward to follow along.
> I've learned a great deal about how Evented I/O systems work, how they're built and when they might be most appropriate (as well as when they're not!)

<em>- Tom Buchok</em>

The previous edition was such a great success, it sold out in just a few days. So if you're interested, book now!

[truthabouteventloops.com](http://truthabouteventloops.com/)
