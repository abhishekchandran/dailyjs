---
layout: post
title: "After Many Years of Desktop Programming..."
author: Alex Young
image: "/images/posts/webglterrain.png"
categories:
- webgl
- graphics
---

If you're interested in WebGL development, then you might enjoy [My forays into JavaScript](http://zephyrosanemos.com/) by Stavros Papadopoulos.  It's basically a paper, WebGL GUI library, and terrain rendering engine all rolled into one fascinating project. The GUI toolkit is desktop and Android inspired, but it's rendered with WebGL.  There's a [live demo](http://zephyrosanemos.com/windstorm/current/live-demo.html) that loads chunks of terrain data as you fly around -- the terrain is rendered offline by a Delphi program.

![Project Windstorm](/images/posts/webglterrain.png)

There are a few things that I found interesting about this project.  The author is a desktop developer that is learning JavaScript, so the demo itself should be encouraging to anyone in the same position.  The screenshots are incredible, and it runs fairly well (I get 30fps on a 2013 MacBook Air).

The section in the article about fetching tiles will be of interest to anyone starting out in WebGL game development.  If you've got server-side experience then designing the API for this is an early problem that you'll have to tackle:

> A very simple and efficient way to determine the potentially visible tiles is by performing a simple intersection test against the bounding box of the viewing frustum's projection on the Y = 0 (horizontal) plane (see first image below).
>
> A slightly more involved but potentially better way (as long as the viewpoint remains above and relatively close to the ground) is to construct our bounding box from the points of the polygon that results from intersecting the frustum with the horizontal plane, combined with the projected points of the frustum's near plane (got that?).

I find the GUI particularly impressive, it's actually pretty usable and I haven't managed to break it yet.  It would be nice if Stavros released it as a library.  I haven't spent much time taking the JavaScript apart yet, so I don't know if he's used any libraries.  In fact, I entered flight mode in the demo and ended up wasting all of my DailyJS writing time for the day!

> All in all, the GUI weighs in at ~12KLOC and spans 24 files, which is quite a bit more than the terrain engine itself!

It sounds like WebGL GUIs can be complicated, depending on your requirements.  In this case I think it was well worth the effort.
