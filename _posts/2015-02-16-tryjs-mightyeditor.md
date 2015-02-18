---
layout: post
title: "TRY.js, MightyEditor"
image: "/images/posts/mightyeditor_screenshot_dailyjs.png"
author: Alex Young
categories:
- games
- tools
- education
---

###TRY.js

When I was at school we had a [turtle graphics game](http://en.wikipedia.org/wiki/Logo_%28programming_language%29) that was meant to teach the rudiments of programming.  It also had a [turtle robot](http://www.classicacorn.freeuk.com/8bit_focus/logo/logo.html) that you could drive around.  There are many attempts to update this type of educational software, but one that impressed me is [TRY.js](https://s-a.github.io/TRY.js/) (GitHub: [s-a/TRY.js](https://github.com/s-a/TRY.js), License: _MIT/GPL_) by Stephan Ahlf:

> TRY.js is supposed to program a virtual robot which moves in a 3D environment and is able to pick up and unload objects. The program gives beginners a first insight into the world of computer programming.
>
> Due to the ease of use and the limited instruction set TRY.js is well suited for the introduction to programming, especially for learning the programming language JavaScript. It gives an overview about synchronous and asynchronous codes as well as test driven development.

It uses Google Drive so you can save your experiments and share them.  There's also a project for [sharing TRY.js packages](https://github.com/s-a/channel.try.js).

If you want to try programming the robot, there's a [Robot API](https://github.com/s-a/TRY.js/blob/master/docs/robot.MD) on GitHub.  Rather than trying to present a fake educational DSL, TRY.js embraces modern JavaScript idioms, so beginners would need assistance but it might help them to learn how people actually write web-based software -- complete with tests!

###MightyEditor

![MightyEditor](/images/posts/mightyeditor_screenshot_dailyjs.png)

Guntis Smaukstelis sent in a powerful web-based game level editor for [Phaser games](http://phaser.io/) called [MightyEditor](http://mightyfingers.com/) (GitHub: [TheMightyFingers/mightyeditor](https://github.com/TheMightyFingers/mightyeditor), [License](https://github.com/TheMightyFingers/mightyeditor/blob/master/LICENSE), [Demo](http://mightyeditor.mightyfingers.com/)).  It supports asset management for organising textures, and there's a map editor so you can paint levels, with tools for scale and rotate. It also has a physics editor and code editing, so you can alter the behaviour of the game without exporting it first.

It's open source with the limitation that you can't create paid services on top of the MightyEditor, and you must reference the project's creator (mightyfingers.com) in your work.  The company behind the editor also sells [paid subscriptions](http://mightyfingers.com/subscriptions/), so you can support them if you use it for building your own games.  Otherwise the licensing is flexible, and it seems like a powerful tool.
