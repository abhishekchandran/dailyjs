---
layout: post
title: "Confused About Components"
author: Alex Young
categories:
- component.json
- package-management
---

Client-side development has been shifting away from monolithic libraries.  While jQuery is still hugely popular, building projects from smaller libraries is increasingly common.  To make this easier to deal with, projects have appeared to manage dependencies.  These tools may be simple package managers, or a combination of a build tool and a package manager.

###Recent History

Client-side package managers have been around for a few years now.  An earlier example is [CPM](https://github.com/kriszyp/cpm), which is a CommonJS package manager.  Last year the subject got newfound attention from Node developers.  There was a very public debate between Isaac Schlueter and TJ Holowaychuk in which several issues were covered:

* Should client-side libraries use CommonJS modules or AMD?
* Should npm or a new registry be used to store client-side libraries?
* What should be included within client-side libraries?

> "A component can be not just JavaScript, but CSS, images, fonts or other resources, or a component may be any combination of these. This is the main idea that I want to sell, we need to broaden modularity beyond just JavaScript source."

-- [TJ Holowaychuk, Components](http://tjholowaychuk.com/post/27984551477/components)

> "However, they should have the same level of modularity and order that we've been able to get with JavaScript packages using npm and Node.js. It's a much stickier problem, because the deployment environment is so much more hostile."

-- [Isaac's response](http://blog.izs.me/post/27987129912/tj-holowaychuk-components)

Shortly after this discussion, TJ released [Component](https://github.com/component/component), which is a _component_ manager.  Components may include JavaScript, styles, and markup.  Markup and styles are encouraged to be "structural", allowing users to easily skin components.  Examples of components include anything from generic JavaScript libraries -- like a small [mathematical helper function](https://github.com/component/mean), to a fully-blown UI widget, like a [date picker](https://github.com/component/datepicker).

###Component Workflows

What isn't immediately obvious about Component is it builds client-side scripts by adding a [CommonJS Modules/1.1](http://wiki.commonjs.org/wiki/Modules/1.1) implementation -- components are loaded using `var lib = require('lib')`.  The upshot of this is there's a learning curve to writing components, and also understanding how to make this work inside existing projects.  Component is specifically designed to work regardless of server-side architecture, so you could use it with Django, Express, or Rails projects without special handling.  Discovering how to use components inside these frameworks is the main point of friction when switching to a component-based workflow -- do you structure your entire project around components?  Or just use Component as a way of managing dependencies?

Contrast this to Bower.  It's more like earlier projects, which include Jam and Volo, and therefore offers less in terms of treating entire slices of the UI as reusable chunks.  This is by design -- Bower is meant to work with build tools rather than replace them.

Then there's Ender, which provides an API for loading modules (CommonJS is supported), and is built on top of npm.  Jam encourages the use of AMD and depends on RequireJS.  Volo doesn't depend on AMD modules, but encourages them to be used.

> Bower could have effectively been: `curl http://wherever-bower-repos-are.com | grep underscore | xargs git clone`

-- [TJ Holowaychuk, component Google Group](https://groups.google.com/d/msg/componentjs/FGM46qQX9hs/edG3KwOIdLYJ)

That's how I initially felt when I first saw Bower, but Bower's simplicity is a result of it being designed to work alongside client-side build tools.  That means Bower will work with RequireJS, LoadBuilder, or even Sprockets.  If you're using a large server-side framework like Rails, then it might be easier to use Bower with the framework's existing asset management tools.

###Build Tools and Package Managers

As TJ hinted at above, the biggest problem facing client-side package managers is anybody can make one.  It doesn't take much effort to write a script that can fetch libraries from GitHub and then pipe them through UglifyJS.

Bower's separation between package manager and build tools is insightful, but I also think the modular client-side development being pushed by Component is extremely important and makes client-side development better.

###The State of Affairs

We're now at the point where library authors are increasingly including a `component.json` file.  How do you know if this is a Bower or Component manifest file?  Let's say I want to install [pjax](https://github.com/defunkt/jquery-pjax).  It has a `component.json`, so I run `component install defunkt/jquery-pjax`.  The result is an error:

{% highlight text %}
error : Error: invalid component name "jquery"
{% endhighlight %}

It turns out pjax is designed to be used with Bower.

This situation is made more confusing because neither project addresses this fact.  It's almost like they don't want to acknowledge each other.  There's a [discussion about Bower](https://groups.google.com/d/msg/componentjs/FGM46qQX9hs/zOryL24q1AcJ) in the component Google Group, but neither project is particularly helpful with regard to the differences between manifest files, given the decision to use the same name.

Is Bower run by evil Twitter imperialists hell-bent on wrestling `component.json` away from the Component project?  Well, no, because Bower can be configured to use a different file name, and the projects have different goals.  However, the clash is unfortunate, particularly for client-side developers who work closer to the design end of the design/coding spectrum, and may not even be aware that both projects exist.

It would be nice to see this issue addressed clearly in Bower and Component's documentation.  The fact Twitter has its logo on Bower doesn't make it the best or correct project to use -- I encourage you to try out both projects.  Client-side development is more than just JavaScript files, so I feel like Component has a chance to reach critical mass if enough people get behind it.

###Jargon

* *Package Manager*: Fetch scripts from online sources like GitHub, taking dependencies into account.
* *Build Tool*: Combine scripts and other assets together into something usable by browsers.
* *Module System*: A way to programmatically load scripts when they're needed.

###Comparison Table

<table class="amy horizontal">
  <thead>
    <tr>
      <th>&nbsp;</th>
      <th><a href="http://twitter.github.com/bower/">Bower</a></th>
      <th><a href="https://github.com/component/component">Component</a></th>
      <th><a href="http://ender.jit.su/">Ender</a></th>
      <th><a href="http://jamjs.org/">Jam</a></th>
      <th><a href="http://volojs.org/">Volo</a></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>License</th>
      <td>MIT</td>
      <td>MIT</td>
      <td>MIT</td>
      <td>MIT</td>
      <td>MIT/New BSD</td>
    </tr>
    <tr>
      <th>Appeared</th>
      <td>Sep 2012</td>
      <td>Aug 2012</td>
      <td>Apr 2011</td>
      <td>May 2012</td>
      <td>Oct 2010</td>
    </tr>
    <tr>
      <th>Package Registry</th>
      <td><a href="http://sindresorhus.com/bower-components/">Server</a></td>
      <td><a href="https://github.com/component/component/wiki/Components">Wiki</a></td>
      <td><a href="https://npmjs.org/">npm</a></td>
      <td><a href="http://jamjs.org/packages/#/">Server</a></td>
      <td>GitHub</td>
    </tr>
    <tr>
      <th>Module Pattern</th>
      <td>&nbsp;</td>
      <td>CommonJS</td>
      <td>CommonJS</td>
      <td>AMD</td>
      <td>AMD/CommonJS compatible</td>
    </tr>
  </tbody>
</table>

