---
layout: post
title: "Databound, Typist"
author: Alex Young
image: "/images/posts/databound.png"
categories:
- libraries
- dom
- ui
- ajax
- rest
- http
---

###Databound

![Databound](/images/posts/databound.png)

If you use Ruby on Rails, then you might like this Rails REST library wrapped: [Databound](http://databound.me/) (GitHub: [Nedomas/databound](https://github.com/Nedomas/databound), License: _MIT_, npm: [databound](https://www.npmjs.com/package/databound), Bower: `databound`) by Domas Bitvinskas.  The API looks a bit like the Rails syntax for database models:

{% highlight javascript %}
User = new Databound('/users')

User.where({ name: 'John' }).then(function(users) {
  alert('Users called John');
});

User.find(15).then(function(user) {
  print('User no. 15: ' + user.name);
});

User.create({ name: 'Peter' }).then(function(user) {
  print('I am ' + user.name + ' from database');
});
{% endhighlight %}

Install it with npm, Bower, or as part of a Rails asset pipeline.  The author also notes that you can use it with Angular as an alternative to `ngResource`.

###Typist

Typist (GitHub: [positionly/Typist](https://github.com/positionly/Typist), License: _MIT_, Bower: _Typist_) by Oskar Krawczyk is a small library for animating text as if it's being typed.  It can work with responsive layouts, and the author claims it has improved click-through-rates on a commercial homepage.

It doesn't have any dependencies, and is invoked by a constructor that accepts options for the animation intervals.  The required markup should specify the text to be typed in the `data-typist` and `data-typist-suffix` attributes.

