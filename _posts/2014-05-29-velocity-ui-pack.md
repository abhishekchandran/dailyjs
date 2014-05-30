---
layout: post
title: "Velocity UI Pack"
author: Alex Young
categories:
- animations
- ui
- jquery
---

Julian Shapiro has announced the [Velocity UI Pack](http://julian.com/research/velocity/#uiPack).  There's a [screencast that introduces the effects](https://www.youtube.com/watch?v=CdwvR6a39Tg&hd=1) and how to use them.

This is an additional dependency for the [Velocity.js library](http://julian.com/research/velocity/), which is a performance-focused jQuery plugin that improves on `$.animate()`.  With the Velocity UI Pack you can perform animations on sets of elements, which is ideal for drawing attention to content as it's loaded using Ajax.

It supports a `stagger` option which adds a delay after each animation.  Given a set of elements, you can apply an animation in sequence simply by using `$divs.velocity('callout.shake', { stagger: 75 })`.  If you're loading an array of records using Ajax, then you can render the resulting elements and display them with `.velocity('anim', { stagger: time })`.

One thing that I like about this library is the animations don't result in blurry text.  Julian has gone to a lot of trouble to make it easy to use and fast, so it's worth checking out [the demo](http://julian.com/research/velocity/#uiPack) and the [screencast](https://www.youtube.com/watch?v=CdwvR6a39Tg&hd=1).
