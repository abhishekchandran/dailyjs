---
layout: post 
title: "Declarative Graphics"
author: Alex Young
categories:
- graphics
- animations
- reactive
- svg
---

Whenever I hear the term 'reactive', I immediately think about data-driven forms and widgets.  Markup isn't just used for HTML forms and widgets, however: SVG is a markup language, so why not use reactive programming techniques to generate data-driven graphics?

That's the goal of Paths.js (GitHub: [andreaferretti / paths-js](https://github.com/andreaferretti/paths-js), License: _Apache 2.0_, bower: _paths-js_), by Andrea Ferretti.  It features a chainable API for generating SVG paths:

{% highlight javascript %}
var path = Path()
  .moveto(10, 20)
  .lineto(30, 50)
  .lineto(25, 28)
  .qcurveto(27, 30, 32, 27)
  .closepath();
{% endhighlight %}

Calling `path.print()` returns the relevant markup.  This can then be used with a templating language like Handlebars or mustache.js: [templates/line.html](https://github.com/andreaferretti/paths-js-demo/blob/3d37cb1566f2043bf9f49e1708d9e8ae41206437/app/templates/line.html).

This example is from [the Paths.js demo](http://andreaferretti.github.io/paths-js-demo/) (GitHub: [andreaferretti / paths-js-demo](https://github.com/andreaferretti/paths-js-demo)).  The demo uses [Ractive.js](http://www.ractivejs.org/) to bind JSON data to UI controls and charts.  It has several graphs with animations, and uses instances of `Ractive` together with instances of `Path` to create a clean, interactive data-driven UI.

<div class="image">
  <img src="/images/posts/pathsjsdemo.gif" alt="" />
  <small>Reactive Pokémon stats.</small>
</div>

I like the combination of modern templating languages, SVG, and Ractive.js in Andrea's demo.  The Paths.js API makes generating SVG less tedious than it could be, and various charts are included that you can use to get started quickly.

If you like the sound of Ractive.js, then take a look at [the Ractive.js demos](http://examples.ractivejs.org/), which include some SVG examples.
