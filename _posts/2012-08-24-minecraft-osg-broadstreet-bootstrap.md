---
layout: post
title: "Minecraft Character WebGL, OpenSceneGraph, BroadStreet, Bootstrap"
author: "Alex Young"
categories: 
- webgl
- threejs
- bootstrap
- backbone.js
---

###Minecraft Character in WebGL

![Minecraft Items demo](/images/posts/minecraftitems.png)

In [Minecraft Character in WebGL](http://learningthreejs.com/blog/2012/07/05/minecraft-character-in-webgl/), Jerome Etienne demonstrates how to render and animate Minecraft characters using his tQuery library.  This was inspired by the [Minecraft Items Chrome Experiment](http://djazz.mine.nu/lab/minecraft_items/).

###OpenSceneGraph

![Mickey point cloud](/images/posts/mickeypointcloud.png)

[OpenSceneGraph](http://osgjs.org/) (GitHub: [cedricpinson / osgjs](https://github.com/cedricpinson/osgjs), License: _LGPL_) by Cedric Pinson is a WebGL framework based on [OpenSceneGraph](http://www.openscenegraph.org/) -- a 3D API typically used in C++ OpenGL applications.  This means it's possible for developers experienced with OpenSceneGraph to bring their projects across to a familiar environment that runs in modern browsers thanks to WebGL.

###BroadStreet

[BroadStreet](http://darrenhurst.github.com/BroadStreet/) (GitHub: [DarrenHurst / BroadStreet](https://github.com/DarrenHurst/BroadStreet), License: _MIT_) by Darren Hurst is a set of controls for Backbone.js.  It includes a list selector, iOS-style toggles and alerts, SVG icons, and labels.

Each control inherits from `Backbone.View.extend`, so the API looks like a standard Backbone object:

{% highlight javascript %}
var toggle = new Toggle('controls', this).render();
toggle.setTitle('Example title');
{% endhighlight %}

The author recommends testing the project with a web server to avoid security restrictions caused when running the examples locally.

###Bootstrap 2.1.0

[Bootstrap 2.1.0](http://blog.getbootstrap.com/2012/08/20/bootstrap-2-1-0-released/) is out:

> New docs, affix plugin, submenus on dropdowns, block buttons, image styles, fluid grid offsets, new navbar, increased font-size and line-height, 120+ closed bugs, and more. Go get it.

The [Bootstrap homepage](http://twitter.github.com/bootstrap/) showcases the new features and has a slight redesign.  Hopefully it'll inspire Bootstrap users to customise their projects a little bit instead of using the same black gradient navigation bar on every single project!
