---
layout: post
title: "s/Ampersand.js/Backbone and Express/"
author: "Alex Young"
categories:
- frameworks
- node
---


[Ampersand.js](http://ampersandjs.com/) from [&amp;yet](http://andyet.com/) is a new web framework.  It follows the trends that I've been using for my own applications:

* Everything is CommonJS
* Client-side dependencies use npm (for a list of modules, see <http://tools.ampersandjs.com>)
* State and data binding is Backbone-inspired

It has a heavy focus on client-side development, so it leans on the MVVM approach.  Most of these ideas come together in the [form documentation](http://ampersandjs.com/learn/forms):

> The quickest way to build out a starting point for a form in your project is to point ampersand-cli at a model file to generate a form for editing it.
> We'll eventually make more "official" input views types. But the idea is, if you want to write a color picker, or a date input view, or a username-checker-input that does server-side validation, or a password field with a strength indicator, you can write a view for that and as long as it follows the form view conventions in the list above and it will still work happily with the rest of the form.

This is further explained explained in [what is a view?](http://ampersandjs.com/learn/view-conventions#what-is-a-view-according-to-ampersand)

> It doesn't matter if your "view" is an instance of ampersand-view or not. Any object can be a view if it follows a few rules.

The example on that page looks like Backbone as well.

When generating a new Ampersand application, it prompts for the server-side module.  You can use either Express or hapi.  It makes a demo app, which almost entirely client-side JavaScript.  The payload that gets served is just this:

{% highlight html %}
<!DOCTYPE html>
<link href="/dailyjs.nonCached.css" rel="stylesheet" type="text/css">
<script src="/dailyjs.nonCached.js"></script>
{% endhighlight %}

It runs using a livereload module, so you can edit files and the client will be updated.  As the documentation says, it treats the browser as a runtime.

Ampersand seems like a way to unify Node and Backbone development.  I don't yet know how well Ampersand works in production on services like Heroku, or how easy it is to test, but I'm definitely enthusiastic about the idea of blending Node and libraries like Backbone or AngularJS.
