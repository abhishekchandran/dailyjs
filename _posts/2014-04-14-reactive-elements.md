---
layout: post
title: "Reactive X-Tags"
author: "Alex Young"
categories: 
- elements
- xtag
---

![Reactive Elements](/images/posts/reactiveelements.png)

Here's a cool idea I haven't seen before: [ReactiveElements with X-Tag](https://github.com/PixelsCommander/ReactiveElements).  [X-Tag](https://github.com/x-tag/core) is a library from Mozilla that uses JavaScript to provide support for the current W3 Web Components draft.  This basically allows modern browsers to use custom elements:

> X-Tag allows you to easily create elements to encapsulate common behavior or use existing custom elements to quickly get the behavior you're looking for.

> X-Tag provides several powerful features that streamline element creation such as: Custom events and delegation, mixins, accessors, component lifecycle functions, pseudos and more.

The [PixelsCommander / ReactiveElements](https://github.com/PixelsCommander/ReactiveElements) project by Denis Radin is a small MIT licensed library that builds on X-Tag so you can use it with [React.js](http://facebook.github.io/react/).

First you create a React component definition:

{% highlight javascript %}
MyComponent = React.createClass({
  render: function() {
    console.log(this.props.items);
    return <ul><li>React content</li></ul>;
  }
});

xtag.registerReact('my-react-component', MyComponent);
{% endhighlight %}

And then you can use `my-react-component` in your HTML and see `items` if it has been specified as an attribute.

I like the idea of combining these two libraries, it has an AngularJS feel while embracing upcoming standards.
