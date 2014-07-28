---
layout: post
title: "Blockies, Angular Debaser"
author: "Alex Young"
categories:
- libraries
- ui
- graphics
- angularjs
- testing
---

###Blockies

Blockies (GitHub: [download13 / blockies](https://github.com/download13/blockies), License: _WTFPL_) by Erin Dachtler is a small library that generates avatars based on a random seed and colour.

{% highlight javascript %}
var icon = blockies.create({
  seed: 'randstring',
  color: '#dfe',
  size: 15,
  scale: 3
});
{% endhighlight %}

The arguments are all optional, and the output is a canvas element that you can insert into a container.  The resulting images look a bit like the default GitHub avatars.

###Angular Debaser

[Angular Debaser](http://decipherinc.github.io/angular-debaser/) (GitHub: [decipherinc / angular-debaser](https://github.com/decipherinc/angular-debaser), License: _MIT_) by Christopher Hiller is a library designed to cut down the amount of boilerplate required to test AngularJS projects.

When a module depends on a lot of services, then it can require a lot of stubs to test.  To get around that, Debaser provides a more succinct syntax:

{% highlight javascript %}]
debaser()
  .module('donny.pizzajoint.admin')
  .object('Settings', {
    location_id: 1
  })
  .object('User').withFunc('getAll').returns([])
  .object('Pizza').withFunc('getAll').returns([])
  .object('Toppings').withFunc('getAll').returns({})
  .object('Sides').withFunc('getAll').returns([])
  .object('Orders').withFunc('getPreviousWeek').returns([])
  .object('Deliveries').withFunc('getPreviousWeek').returns([])
  .debase();
{% endhighlight %}

It uses [angular-mocks](https://github.com/angular/bower-angular-mocks), which is "ngMock" from the main AngularJS project.
