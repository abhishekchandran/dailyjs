---
layout: post
title: "Node Roundup: newspeak, CatchMe, Catnap"
author: "Alex Young"
categories:
- node
- npm
- modules
- email
- REST
---

###newspeak

newspeak (GitHub: [yoshuawuyts / newspeak](https://github.com/yoshuawuyts/newspeak), License: _MIT_, npm: [newspeak](https://www.npmjs.org/package/newspeak)) by Yoshua Wuyts is a module inspired by [Mozilla's L20n](http://l20n.org/) project:

> L20n is a new localization framework developed by Mozilla for the Web. It allows localizers to put small bits of logic into localization resources to codify the grammar of the language.

The following example is a small pluralisation helper:

{% highlight javascript %}
var newspeak = require('newspeak');
l20n.currentLanguage('nl');
var l20n = newspeak({ language: 'nl', gender: 'male' });

var data = {
  users: function(obj) {
    if (0 === obj.count) return 'nobody';
    if (1 === obj.count) return 'someone';
    return '{{count}} people';
  }
};

l20n.register({ nl: data });
l20n.get('users', { count: 3 });
{% endhighlight %}

###CatchMe

CatchMe (GitHub: [Pentiado / catch-me](https://github.com/Pentiado/catch-me), License: _MIT_, npm: [catch-me](https://www.npmjs.org/package/catch-me)) by Paweł Wszoła is another Node SMTP server that captures emails.  This one has a nice web interface, and can validate email with Campaign Monitor.

It accepts command-line arguments for defining the web and SMTP ports: `catchme --mailPort 1234 --appPort 4321`

###Catnap

Catnap (GitHub: [mikaa123 / catnap](https://github.com/mikaa123/catnap), License: _MIT_, npm: [catnap](https://www.npmjs.org/package/catnap)) by Michael Sokol is an Express-compatible module for generating REST resources:

{% highlight javascript %}
var makeResource = require('catnap').makeResource;

var userResource = makeResource('user', '/users/:userId')
  .representation(function(user) {
    // The default representation. Returns a full representation of user
    return user;
  })
  .representation('partial', function(user) {
    // A named representation that returns a partial representation
    return pick(user, 'username', 'email');
  })
  .get(function(req, res) {
    // Action methods take standard middleware.
    User.findOne({ _id: req.params.userId }, function(err, user) {
      user && res.send(200, userResource(user));
    });
  })
  .attachTo(app);
{% endhighlight %}

There's a [wiki with documentation](https://github.com/mikaa123/catnap/wiki/Getting-Started) that explains how the module relates to Roy Fielding's dissertation:

> So in other words, a resource is some service that lives at a URI and that has one or more representations. In order to interact with a resource, we need to use an HTTP request method, you know, GET, POST, PUT, PATCH and DELETE. These methods have a lot of semantics baked in! For example, when we GET /users/123, we are asking for the representation of the user who's id is '123'. This HTTP transaction (request-response) is called an action.

