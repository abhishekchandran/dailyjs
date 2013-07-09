---
layout: post
title: "jQuery Roundup: Selleckt, Drag and Drop AngularJS, jqfactory"
author: Alex Young
categories:
- jquery
- plugins
- jqueryui
- widgets
- angularjs
- select
---

<div class="intro">
Note: You can send your plugins and articles in for review through our <a href="http://contact.dailyjs.com/project">contact form</a>.
</div>

###Selleckt

[Selleckt](http://brandwatchltd.github.io/selleckt/demo/) (GitHub: [BrandwatchLtd / selleckt](https://github.com/BrandwatchLtd/selleckt), License: _MIT_) by Graham Scott is another `select` replacement.  This one comes with Mocha tests, multiple select support, mustache.js for templating, and works as an AMD module or jQuery plugin.

The basic syntax (taken from the demo page) looks like this:

{% highlight javascript %}
$select3.selleckt({
  mainTemplate: fancyTemplate,
  selectionTemplate: selectionTemplate,
  selectedClass: 'selected',
  selectedTextClass: 'selectedText',
  itemsClass: 'items',
  itemClass: 'item'
});
{% endhighlight %}

There are tonnes more options which are documented in the project's readme on GitHub.

###Drag and Drop for AngularJS

[Drag and Drop for AngularJS](http://codef0rmer.github.io/angular-dragdrop/#/) (GitHub: [codef0rmer / angular-dragdrop](https://github.com/codef0rmer/angular-dragdrop), License: _MIT_) by Amit Gharat is an AngularJS directive for [jQuery UI's Draggable Widget](http://api.jqueryui.com/draggable/).

It supports draggable items and droppable targets, and activity can be observed using a controller's `$scope`.  The markup for the relevant directives looks like this:

{% highlight html %}
<div class="btn btn-primary" data-drag="true" data-jqyoui-options="{revert: 'invalid'}" ng-model="list1" jqyoui-draggable="{animate:true}" ng-hide="!list1.title">{{list1.title}}</div>
{% endhighlight %}

The project comes with a Grunt build script and unit tests.

###jqfactory

jqfactory (GitHub: [gfranko / jqfactory](https://github.com/gfranko/jqfactory), License: _MIT_) by Greg Franko is an API for building stateful jQuery widgets.  It's inspired by the jQueryUI widget factory, and supports jQuery prototype namespacing support, deferred/promises, clean event binding and clean up, and AMD.

The project's readme contains a walkthrough that demonstrates how to wrap your code in Greg's API.  Here's a snippet that shows how to support options, the constructor, and reinitialisation:

{% highlight javascript %}
(function($, window, document, undefined) {
    // Your plugin will go here
    // namespace - person
    // name - greg
    $.jqfactory('person.greg', {
        // Your plugin instance properties will go here
        // Default plugin options
        options: {
            occupation: 'JavaScript Engineer',
            age: 24
        },
        // Plugin Constructor
        _create: function() {
            // This is where you can set plugin instance properties
            this.fullname = 'Greg Franko';
        },
        // Plugin re-initialized
        _init: function() {
            // You can include any logic that you like when your plugin constructor is re-called
        }
    }
    });
}(jQuery, window, document));
{% endhighlight %}

The project includes more documentation, a Grunt build script, and Jasmine tests.
