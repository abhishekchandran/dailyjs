---
layout: post
title: "Angular Selection Model, Normalized Particle Swarm Optimization"
author: Alex Young
categories:
- graphics
- optimisation
- angularjs
---

###Angular Selection Model

[Angular Selection Model](http://jtrussell.github.io/angular-selection-model/) (GitHub: [jtrussell / angular-selection-model](https://github.com/jtrussell/angular-selection-model), License: _MIT_) by Justin Russell is an AngularJS directive for managing selections of items in lists and tables.  It's indifferent to how data is presented, and only tracks what items are selected.

This example allows a text input to filter a list of items, and also allow the user to select items from the list:

{% highlight html %}
<input type="text" ng-model="fancyfilter" />

<table>
  <thead>
    <tr>
      <th></th>
      <th>#</th>
      <th>Label</th>
      <th>Value</th>
    </tr>
  </thead>
  <tr ng-repeat="item in fancy.bag | filter:fancyfilter"
      selection-model
      selection-model-type="checkbox"
      selection-model-mode="multiple-additive"
      selection-model-selected-class="foobar">
    <td><input type="checkbox"></td>
    <td>1</td>
    <td></td>
    <td></td>
  </tr>
</table>
{% endhighlight %}

The directive does a lot of things behind the scenes to make this work naturally.  An internal read-only list is used to represent selected items, and there's a provider for setting things like the selected attribute and class name assigned to selected items at a global level.  Checkboxes are automatically managed, including support for multiple selection.

Justin has included tests, documentation, and examples.

###Normalized Particle Swarm Optimization

![Swarm optimisation](/images/posts/pso-anim.gif)

Adrian Seeley sent in this gist: [JavaScript Normalized Particle Swarm Optimization Implementation](https://gist.github.com/adrianseeley/9155206).  If you want to try it, just click "Download Gist" then open the HTML file locally.

The reason I wanted to write about it was he decided to license it as "Abandoned", so rather than letting it languish I thought I'd share it in case someone finds it useful.

Here's how Adrian described the project:

> Particle swarm optimization is an incredibly viable machine learning structure, but is often implemented using database oriented designs splayed across multiple files in c++ or java making it very inaccessible to newcomers.
>  I present a simple, unoptimized, and easy to follow javascript implementation of normalized particle swarm optimization, making use of full descriptive variable names entirely encapsulated in a single inlined function.

