---
layout: post
title: "Tetris with WebSockets"
author: Alex Young
categories:
- games
- node
- websocket
---

<div class="image">
  <img src="/images/posts/tetris-websockets.png" />
  <small>Tetris with WebSockets.</small>
</div>

A few weeks ago I ran an introductory Node workshop at [Makers Academy](http://www.makersacademy.com/):

> Makers Academy is a highly selective, 12 week full-time programme that teaches web development in London. We accept only the top applicants onto the course for a rigorous programme that culminates with the graduation day when we introduce them to London's top technology companies looking to hire entry-level developers.

The workshop had a 50 minute talk where I introduced Node, then we set the students a challenge: improve our [Tetris game](https://bitbucket.org/alexyoung/tetris).  The challenges started at basic UI improvements and ended at intermediate Node web development.

To make the game, I created a [small Tetris game engine](https://www.npmjs.org/package/sirtet) -- using test-driven development, naturally.  The idea behind the game and workshop was to get people thinking about what Node is good at, but we also had an ulterior motive: recruitment.  We were struggling to hire a web junior web developer with Node skills, so Makers Academy provided us with a unique opportunity to talk to some enthusiastic new developers.

I've written a more detailed post about the workshop on Medium: [An introductory Node workshop at Makers Academy](https://medium.com/p/f80195005276).  I enjoyed writing the game engine as a Node module, and it made me want to try making a bigger WebSocket powered game... (when my book is finished!)
