---
layout: post
title: "Definitive Guide to Generators, Golden Layout"
author: "Alex Young"
image: "/images/posts/goldenlayout.png"
categories:
- libraries
- design
- layouts
- articles
---

###Definitive Guide to Generators

Gajus Kuizinas read through many ES6 generator articles before he understood them properly.  I admit I've had the same problem: beyond the basic API, how do you do things like delegate `yield` statements, or raise and handle errors?  And even with a good understanding of the API it can be hard to know when to use generators.

This confusion resulted in Gajus writing [a detailed article about generators](http://gajus.com/blog/2/the-definetive-guide-to-the-javascript-generators#building-an-iterator-from-a-generator).  It has lots of examples, including a handy gif that illustrates the flow of execution in a debugger.

Gajus' article covers pretty much everything I can think of, but even so I think it would be nice to see more practical examples to show you generators can improve real world code.  I've been looking at how [Koa](http://koajs.com/) projects use generators by searching for open source apps on GitHub, so that can be a useful way to see how people are using them.

###Golden Layout

![Golden Layout](/images/posts/goldenlayout.png)

If someone says "build me an admin area!" or "we need a dashboard!" I immediately reach for Bootstrap.  But there are other options, and some may be a better fit depending on what you're working on.  [Golden Layout](https://golden-layout.com/) is a new "layout manager" for web applications that supports resizable windows.

It reminds me a little bit of an X11 window manager, a concept that has been tried many times in web development but has always felt a little unnatural.  The examples in Golden Layout feel fast and precise -- there are no messy gradients or shadows.  It may work well for projects that need to adapt to user generated data.  This could be something like displaying tables or graphs, like an analytics tool or dashboard.

The [examples](https://golden-layout.com/examples/) include Highcharts, SlickGrid, and Angular.  The [tutorials](https://golden-layout.com/tutorials/) expand on this further with RequireJS and more complex Angular projects.

This project is [CC BY-NC 4.0](http://creativecommons.org/licenses/by-nc/4.0/), so you'll need to license it for commercial use.  It's created and maintained by Hoxton One Ltd, a company based in London, and the source is on GitHub: [hoxton-one / golden-layout](https://github.com/hoxton-one/golden-layout).
