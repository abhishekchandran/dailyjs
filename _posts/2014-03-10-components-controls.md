---
layout: post
title: "Introducing Web Components to Control Authors"
author: Matthew Phillips
categories:
- components
- tutorials
---

<div class="intro">This is a guest post by Matthew Phillips, from <a href="http://bitovi.com/">Bitovi</a>.  You can find him on Twitter: <a href="http://twitter.com/matthewcp">@matthewcp</a> and GitHub: <a href="https://github.com/matthewp">matthewp</a>.</div>

At this point unless you've been living under a rock you've likely heard at least a little about web components, a collection of emerging standards created with the intent of making web development more declarative. Among other things, web components allow for custom elements, an easier way to encapsulate your widgets. If you've been developing with MVC frameworks there is a learning curve to using components, but once things start to click you'll want to use them everywhere in your application. Who hasn't wanted an easy way to insert a random cat picture?

{% highlight html %}
<randomcat width="200" height="300"></randomcat>
{% endhighlight %}

<img src="http://placekitten.com/g/200/300"/>

Creating widgets that are well encapsulated is something we do on a daily basis on as JavaScript engineers. In this article I'll explain where traditional control-based MVC has fallen short of that goal and how web components can resurrect the ease of development from the web's early roots.

## MVC's Brick Wall

Traditional MVC frameworks encourage you to organize your view code by creating constructor functions called Controls or Views. If you've developed in this way you probably recognize some of the problems you encounter with this approach.

### Tracking Down Instantiation

Since Controls are implemented as constructor functions that operate on a template, any sub view must be manually instantiated within one of the control's lifecycle methods, usually either init or render. Consider the following in Backbone:

{% highlight javascript %}
var Widget = Backbone.View.extend({
  initialize: function() {
    this.subView = new InnerWidget({ el: $('#inner') });
  },

  render: function() {
    this.$el(this.template());
    this.subView.render();
  }
});
{% endhighlight %}

That's a lot of code that will become more complex as you add additional subviews or conditions for rendering.

### (Lack Of) External API

While creating a widget, its common to create an external API to interact with.  With traditional MVC controls, there is no standard way to do this, so it ends up being ad-hoc at the whim of the author.  For example, here's an accordion containing Panel subviews:

{% highlight javascript %}
var PanelView = Backbone.View.extend({
  template: _.template($('#panel-tmpl').html()),

  render: function() {
    this.$el.html(this.template(this.model.toJSON()));
    return this.$el;
  }
});

var AccordionView = Backbone.View.extend({
  template: _.template($('#acc-tmpl').html()),

  addPanel: function() {
    if (panel instanceof PanelView) {
      this.$el.find('.panels').add(panel.render());
    }
  }
});
{% endhighlight %}

And then to use this:

{% highlight javascript %}
var panel = new PanelView({ model: data });
accordion.addPanel(panel);
{% endhighlight %}

You'll want to abstract some of these pain points to create your own "standard API" for controls. You'll probably create some base classes with stub functions for common tasks. Pretty soon you've created your own mini-framework. We're learned to put up with these little things and they don't bother us day-to-day, but when you discover a better way it will change the way you architect your application.

### Hidden Model

Similarly, widgets commonly need to interact with external model data.  Most MVC frameworks provide some way to pass data into the control so a lot of people have established a pattern of passing in a "model" property to fill this hole. Having a clearer way of setting the model for a control opens a lot of doors in terms of composability. With the traditional control pattern you usually wind up using an adhoc ViewModel created with some properties passed in to the constructor and some created as part of the control's own logic.

##Enter Web Components

Web Components are a W3C spec for an HTML and JavaScript construct that, at its heart, is a way to define custom HTML elements.  The spec includes:

* Native templates ([spec](https://dvcs.w3.org/hg/webcomponents/raw-file/tip/spec/templates/index.html))
* A way to load them ([spec](http://w3c.github.io/webcomponents/spec/imports/))
* A method to define custom elements and extend existing ones ([spec](http://w3c.github.io/webcomponents/spec/custom/))
*  Hooks to run functions when an element is inserted in the page.

A custom element can be as complex as the main router for single page application, a simple widget to display markdown inline:

{% highlight html %}
<x-markdown table-of-contents-depth="2">
# Heading

## Sub-heading

* List item
   - Sub list item
</x-markdown>
{% endhighlight %}

or as simple as a way to embed a YouTube video.

{% highlight html %}
<rick-roll></rick-roll>
{% endhighlight %}

Web Components provide an alternate way to define traditional MVC based controls, with several key advantages.

### Maximal Encapsulation

The power of web components is their ability to easily encapsulate the details of a widget while still maintaining the ability to compose them together, thanks to the legacy of HTML's document-oriented roots. Because it is layout-based, web components can be neatly organized in templates, solving the instantiation problem that a control-based workflow suffers from. Applications can become more template driven rather than instantiating controls with complex event handler logic. Let's say you were A/B testing a feature, you could have your template (in Mustache) look something like this:

{% highlight html %}
{% raw %}
{{if randomlyPicked}}
  <rick-roll></rick-roll>
{{/if}}
{% endraw %}
{% endhighlight %}


### Obvious API layer

The API layer for web components is easy to understand. Data is passed to components through HTML attributes.

{% highlight html %}
<x-injector href="/some-page.html" />
{% endhighlight %}

Layout is passed through the element's inner content, as shown in the markdown example above.

### Models and Templates

The web components spec includes templates for the first time in the web's history. This means no more script tag or hidden div hacks to include templates on a page. Templates allow you to create fragments of markup to be used by your components later. They are parsed, but not rendered until inserted into the page.

Models can be bound to the templates, and, through the power of `Object.observe` changes in the model, would result in relevant parts of the template being automatically rendered. If you've used an MVC framework with template binding and observable models you're probably already familiar with this.

Models are passed into components the same way as all types of data, through attributes. 

With CanJS' `can.Component` you can pass the name of your model through the attributes and get the live-binding today, without waiting for standardization to flesh out that part of the spec. This brings me to my last point…

### Using Web Components today

Despite this being early days for Web Components, there are already a few options if you are interested in getting started. Polymer and X-Tags are two projects started by Google and Mozilla engineers working on the Web Components spec. These projects are bleeding-edge and break compatibility often. Additionally they don't attempt to extend the spec with functionality that won't eventually end up in it. What they do offer you is the ability to start using components the way they will be used when browsers have fully implemented the specifications. can.Component, on the other hand, is an early implementation of Web Components that provides additional functionality that is beyond the scope of custom elements.

can.Component adds two-way binding between a component's model (which is not yet part of the web component spec) and its form elements. Additionally it adds declarative binding to a component's templates through it's scope object. Scope is an object that is used to render the template, but with the addition of declarative binding it does much more than that. The scope can be used to update the state of a component and respond to events. Here's a typical example of can.Component that shows off all of these features:

Usage:

{% highlight html %}
<color-selection></color-selection>
{% endhighlight %}

Implementation:

{% highlight javascript %}
{% raw %}
<script id="color-section-template" type="text/mustache">
  <form>
    <span class="validations">{{validationMessage}}</span>
    <input name="name" type="text" can-value="color" can-change="validate">
  </form>
</script>
{% endraw %}
{% endhighlight %}

This is the component's JavaScript:

{% highlight javascript %}
can.Component.extend({
  tag: "color-selection",
  template: can.view("#color-selection-template"),
  scope: {
    color: "blue",
    validate: function() {
      if (!isAColor(this.attr("color"))) {
        this.attr("validationMessage", "Not a valid color");
      } else {
        this.removeAttr("validationMessage");
      }
    }
  }
});
{% endhighlight %}

### We Still Need Libraries

I hope I've demonstrated the way in which web components breaks some of the boundaries we've hit with traditional control-based MVC. At the same time the specification is intentionally low level and leaves room for libraries to improve upon the experience, as can.Component is doing today.

As a consequence of Web Component's inherent declarative nature your code will become more condensed, with far less boilerplate. We're truly approaching a paradigm where separation of concerns is being achieved. But you can't appreciate the way web components changes the way you write applications until you try it yourself. So I encourage you to choose a library and start on your first widget today.

## Further (required) Reading

* [Presentation by Eric Bidelman](http://html5-demos.appspot.com/static/webcomponents/index.html)
* [Presentation by Ryan Seddon](http://ryanseddon.github.io/web-components/)
* [Introduction to Web Components](http://www.w3.org/TR/components-intro/)
