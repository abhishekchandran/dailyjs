---
layout: post
title: "Slideshow, Unity and JavaScript"
author: "Alex Young"
image: "/images/posts/unityjs.png"
categories:
- games
- slideshows
- node
- modules
- tutorials
---

###Slideshow

What do you do when Apple and Microsoft do everything they can to pull us into their walled development environment gardens?  One answer is to unify both environments using a sane Node API.  Ralf S. Engelschall sent in Slideshow (GitHub: [rse / slideshow](https://github.com/rse/slideshow), License: _MPL_, npm: [slideshow](https://www.npmjs.org/package/slideshow)), a module for remote controlling and monitoring presentation programs like PowerPoint and Keynote.

He also wrote [slideshow-forecast](https://www.npmjs.org/package/slideshow-forecast), which is a cool CLI and GUI for monitoring slideshows:

> The motivation for this is that for large presentations which have to be given in multiple variants for different timeslots it is very hard to determine the later presentation duration during preparation time. Instead of performing lots of different dry-runs after each preparation, this tool provides a duration prognosis already during preparation time.

The `slideshow` command-line program itself lets you drive an application with commands like `boot`, `open file`, and `start`.  You can also `goto` a given slide and `stop` the presentation at the end.

Internally it uses Microsoft's `cscript` or Apple's `osascript` to communicate with the target application, so you don't have to worry about strange AppleScript or COM incantations.

###How to Make a 2D Space Shooter in Unity

![Unity](/images/posts/unityjs.png)

The Unity game engine is hugely popular with game developers.  Many of the indie games that I've enjoyed have been made with it, and if I had the time I'd love to make something with it.  I was aware Unity supports C#, but I didn't know [it has a compiled JavaScript language](http://wiki.unity3d.com/index.php/Head_First_into_Unity_with_UnityScript) as well.

Thomas Palef has written a new tutorial about using JavaScript with Unity called [How to Make a 2D Space Shooter in Unity](http://blog.lessmilk.com/unity-spaceshooter-1/).  It shows you how to get started making a game with Unity's UI, and includes some simple JavaScript for handling firing a bullet.

If you're interested in Unity but thought it was something that only desktop developers can get into then you might enjoy following this tutorial.
