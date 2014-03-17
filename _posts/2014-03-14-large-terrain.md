---
layout: post
title: "Rendering Large Terrain in WebGL"
author: Alex Young
categories:
- webgl
- graphics
---

[Rendering large terrains](http://www.pheelicks.com/2014/03/rendering-large-terrains/) by Felix Palmer is a tutorial that demonstrates how to render terrain with a variable level of detail.  There's a [demo](http://felixpalmer.github.io/lod-terrain/) and the [source is on GitHub](https://github.com/felixpalmer/lod-terrain).  It's built with three.js, and is based on a [paper on level-of-detail distribution](http://www.vertexasylum.com/downloads/cdlod/cdlod_latest.pdf).

![Terrain](/images/posts/terrain-lod.png)

> A simple way to do better is to split our plane into tiles of differing sizes, but of constant vertex count. So for example, each tile contains 64×64 vertices, but sometimes these vertices are stretched over an area corresponding to a large distant area, while for nearby areas, the tiles are smaller.

The code uses [GLSL](http://en.wikipedia.org/wiki/OpenGL_Shading_Language), but the main [app/ JavaScript code](https://github.com/felixpalmer/lod-terrain/tree/master/js/app) is all neatly organised with RequireJS, so it's surprisingly easy to navigate and understand.  The tutorial blog post also makes some of these difficult ideas more accessible, so I thoroughly recommend checking it out.
