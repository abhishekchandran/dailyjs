---
layout: post
title: "Node Roundup: npm CLI Roadmap, Nodemailer, Jasmine-Utils"
author: "Alex Young"
categories:
- node
- npm
- modules
- libraries
- jasmine
- testing
- email
---

###npm CLI Roadmap

On the npm blog, there's a post about [the command-line tool's roadmap](http://blog.npmjs.org/post/91303926460/npm-cli-roadmap-a-periodic-update):

> The first piece of redesign work we're tackling is the npm cache. ... The next goal is to turn it into a module with no dependencies on the rest of npm or npmconf and to test the heck out of it.
> As npm moves to being a part of the toolchain of front-end developers (who are more interested in shipping features than figuring out what's going on with their OS), it's time to work on making npm easier to understand when things go wrong.

The article also mentions a better search interface, which I'd like to see because the current CLI search implementation is inflexible.  It's interesting to read about how the project is evolving away from Isaac's original lightweight implementation intended for experts -- the team behind the project has recognised that npm is used by a diverse range of developers.

###Nodemailer

[Nodemailer](http://www.nodemailer.com/) (GitHub: [andris9 / Nodemailer](https://github.com/andris9/Nodemailer)), License: _MIT_, npm: [nodemailer](https://www.npmjs.org/package/nodemailer) 1.0 is out!  This is a complete rewrite, and partly breaks backwards compatibility so you may need to upgrade carefully:

> The new version allows you to write custom plugins for manipulating the outgoing messages. It is also possible to send huge attachments with ease (in the size of tens of gigabytes) thanks to the Streams2 support - even though no one probably needs to send such attachments since probably no e-mail server would accepts these.

###Jasmine-Utils

Jasmine-Utils (GitHub: [mjeanroy / jasmine-utils](https://github.com/mjeanroy/jasmine-utils), License: _MIT_, npm: [jasmine-utils](https://www.npmjs.org/package/jasmine-utils)) by Mickael Jeanroy is a set of custom matchers for Jasmine.  They're grouped around types, like `toBeABoolean` and `toBeDateBefore`.  Methods are included for booleans, strings, arrays, dates, objects and functions:

{% highlight javascript %}
it('should check that an object contains keys', function() {
  var obj = {
    id: 1,
    name: 'foo'
  };

  expect(obj).toHaveKeys('id', 'name');
  expect(obj).not.toHaveKeys('foo', 'bar');
});
{% endhighlight %}

It also includes some handy spy methods, like `jasmine.spyAll` and `jasmine.spyIf`.  These allow objects to be watched to ensure the expected methods are run.

The project includes a huge amount of matchers, so if you're using Jasmine you may want to check it out.
