---
layout: post
title: "Function Plot, Custom Elements Tutorial"
author: Alex Young
image: "/images/posts/function-plot.png"
categories:
- d3
- graphics
- charts
- libraries
- webcomponent
---

###Function Plot

![Function Plot](/images/posts/function-plot.png)

[Function Plot](http://maurizzzio.github.io/function-plot/) (GitHub: [maurizzzio/function-plot](https://github.com/maurizzzio/function-plot), License: _MIT_, npm: [function-plot](https://www.npmjs.com/package/function-plot)) by Mauricio Poppe is a D3-based charting library that is designed to allow you to render functions with as little configuration as possible.

It supports interactive line charts and scatterplots.  I noticed you can change the scale with the mouse scrollwheel, and the effect is extremely cool: it feels very responsive with my Magic Mouse, which I've seen behave weirdly with some web-based graphical libraries.

The readme has a full list of the supported options, but the basic usage is just to supply a target selector and plotting function.  Here's an example:

{% highlight javascript %}
functionPlot({
  target: '#linear',
  data: [{
    fn: function(x) {
      return x * x;
    }
  }]
});
{% endhighlight %}

The library is very Node-friendly, so you can find the module on npm and it'll work fine with Browserify.

###Using Custom Elements to Solve Simple Problems

Mike Macaulay sent in a tutorial about [Custom Elements](http://michaelmac.org/semantic-ui,/custom-elements,/ampersand,/backbone/2015/04/08/custom-elements-to-solve-simple-problems.html) that explains what they are, how to use them, and what their limitations are:

> Webcomponents always seem just over the horizon, really cool but not quite ready to use in production. I'm starting to worry that the full spec never will, as we continue to get nothing but silence from IE and Safari. However, I'm here to tell you about something that does seem ready to go today, Custom Elements.
>
> The whole point of making your own Custom Elements, beyond making your HTML more semantic, is that you can add your own behavior or methods to those elements. This can be useful, as long as we don't try to do too much.

Most people are discovering these new APIs through libraries like React, and there seems to be some confusion about what custom elements are.  Mike's article is a good introduction, and I found the [MDN Web Components](https://developer.mozilla.org/en-US/docs/Web/Web_Components) article is very helpful as well.
