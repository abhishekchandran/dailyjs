---
layout: post
title: "Voyeur, Page Notes, Validator"
Author: Alex Young
categories:
- dom
- selector
- tooltips
- browser
- node
- validation
- libraries
---

###Voyeur

![Voyeur](/images/posts/voyeur.png)

[Voyeur](http://dunxrion.github.io/voyeur.js/) (GitHub: [dunxrion / voyeur.js](https://github.com/dunxrion/voyeur.js), License: _MIT_) by Adrian Cooney is a DOM traversal and manipulation library.  It creates `window.Voyeur`, which wraps around `document.body`.  Then `Object.defineProperty` is used to add getters to nodes that are accessed through `Voyeur`.  That means `Voyeur.element.child.child.fn()` can be used to access elements and perform operations on them.  Elements can be created with the same syntax.

Methods are provided for working with elements.  For example, `use` allows several operations to be performed on the same element:

{% highlight javascript %}
Voyeur.div.ul.li.use(function(li, i) {
  li.innerText = 'Hello';
});
{% endhighlight %}

Tags can be inserted by using the `create` method, and this can be combined with `use`:

{% highlight javascript %}
Voyeur.ul.li.eq(3, 9).use(function(li, i) {
  li.create.em.innerText = 'Emphasized text!';
});
{% endhighlight %}

The author has included tests and a Grunt build script.

###Page Notes

[Page Notes](http://pagenotes.com/pagenotes/tooltipTemplates.htm) ([pagenotes.js](http://pagenotes.com/pagenotes/pagenotes.js), License: _MIT_) by Jim Williams is a client-side script for working with a flexible implementation of tooltips that support rich annotation-like styles:

> Page notes are a very general, highly intuitive generalization of tooltips. When the mouse stops over a tooltip target, a target annotation is embedded in a tooltip skin and displayed according to a placement specification. The skin together with the placement specification constitute the tooltip template. And the resulting displayed tooltip is the page note. No user-supplied JavaScript is involved.

Since tooltips are HTML fragments, they can also contain tooltips, which allows the library to support nested annotations.  Attributes are used to configure tootips.  For example, `placement` can be used to position the container.

###Validator

Validator (GitHub: [Nijikokun / Validator](https://github.com/Nijikokun/Validator), License: _MIT_, npm: [schema-validator](https://npmjs.org/package/schema-validator)) by Nijiko Yonskai is a Node module with browser support that allows data to be validated using a simple JSON schema:

{% highlight javascript %}
var schema = {
  username: {
    type: 'String',
    required: true,
    length: {
      min: 3,
      max: 36
    },
    test: /^[a-z0-9]+$/gi
  }
};

var validator = new Validator(schema);
var check = validator.check({
  username: 'Niji%kokun'
});

console.log(check);
{% endhighlight %}

The `Validator` constructor can return an object that will work as Express middleware, which allows routes to validate data and populate the `req.validated` property.  New validators can be added using `Validator.implement`.

