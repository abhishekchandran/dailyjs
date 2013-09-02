---
layout: post
title: "ChocolateChip-UI, Bootstrap Grid Builder, Bootstrap 3 Performance"
author: "Alex Young"
categories: 
- libraries
- bootstrap
- performance
- benchmarks
- ui
- mobile
---

###ChocolateChip-UI

![ChocolateChip-UI](/images/posts/chui.png)

[ChocolateChip-UI](http://www.chocolatechip-ui.com/) (GitHub: [sourcebitsllc / chocolatechip-ui](https://github.com/sourcebitsllc/chocolatechip-ui), License: _BSD_) from Sourcebits is a new UI framework for mobile web applications that is designed to look like iOS 7, Jelly Bean, and Windows Phone 8.

ChocolateChipUI uses specific HTML5 tags for structural markup.  The `article` element is the "basic building block of ChocolateChip-UI":

> Every article should have a unique id so that it can be identified by the navigation system. These must be valid HTML ids. At load time, ChocolateChip-UI checks to see if you have manually set the navigation state of your articles. If not, it will set the first article as current and the others as next. This will mean that initially you app may momentarily load in a state of disarray before it is arranged properly. As such, we strongly recommend that you always put a state on each article so that it loads correctly.

It uses its own JavaScript framework instead of a more established library, and is based around event-based widgets.  It has some low-level features like touchscreen gesture recognition, but also includes higher-level widgets like `UISegmented`, `UIPopup`, and so on.

The authors have written a guide on how to [transition from jQuery](http://www.chocolatechip-ui.com/documentation#/jquery2chocolatechip):

> ChocolateChipJS is very similar to jQuery. But it's also much smaller. Uncompressed it's just 60kb and compressed, 26kb. In contrast, jQuery is 2.0.3 uncompressed is 242kb and compressed, 84kb. ChocolateChip was designed for modern mobile browsers. It has no legacy code for browser not on current mobile devices.

###Bootstrap Grid Builder

Jay Kanakiya's [Bootstrap Grid Builder](http://jaykanakiya.com/bootstrap-grid-builder/) (GitHub: [kanakiyajay / bootstrap-grid-builder](https://github.com/kanakiyajay/bootstrap-grid-builder), License: _Apache 2.0_) is a tool for exploring and generating column/row grids based on Bootstrap 3's new markup.

It allows you to switch between different devices so you can see what a given layout will look like on a phone, tablet, or desktop.

###Bootstrap 3 Performance

Parashuram Narasimhan sent in [Bootstrap Performance using telemetry](http://nparashuram.com/bootstrap-perf/) and an article about it: [Bootstrap - Evolution over two years](http://blog.nparashuram.com/2013/08/bootstrap-evolution-over-two-years.html):

> The performance drop seems to stop at 2.3.2 release and looks like the latest 3.0.0 release was aimed at making things faster. A lot of components in 3.0.0 are way better than their 2.3.2 counterparts.

> There are significant performance changes between the RC and the final versions of 3.0.0. This could be due to incorrect CSS files I generated, or was there something different in the final release?

The telemetry page allows you to view performance metrics for each Bootstrap component for each point release.
