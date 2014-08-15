---
layout: post
title: "Js13kGames, Angular Plasmid"
author: "Alex Young"
categories:
- games
- competitions
- graphics
- biology
- angularjs
- testing
---

###Js13kGames

Andrzej Mazur wrote in to say that the [Js13kGames competition](http://js13kgames.com/) has started.  All entries must be in by the 13th of September.  It's a competition to build HTML5 games in 13 kilobytes, and that includes all assets. If you want sounds and complex graphics then it might be advantageous to procedurally generate certain things.

> All your code and game assets should be smaller than or equal to 13 kilobytes (that's exactly 13,312 bytes, because of 13 x 1024) when zipped. Your package should contain index.html file and when unzipped should work in the browser.

The competition has a theme, so entries should somehow encapsulate the elements:

> The main theme of the competition in 2014 is The Elements: Earth, Water, Air and Fire. It is optional, so you can use it, use part of it (one Element), or drop it. Remember that there will be bonus points for implementing the theme in your game.

Andrzej wrote a tutorial for tuts+ about [minifying games](http://gamedevelopment.tutsplus.com/articles/how-to-minify-your-html5-game-for-the-js13kgames-competition--cms-21883), and he created the game [Triskaidekaphobia](http://enclavegames.com/games/triskaidekaphobia/) to promote the competition.

###Angular Plasmid

![Angular Plasmid](/images/posts/angularplasmid.png)

[Angular Plasmid](http://angularplasmid.vixis.com/) (GitHub: [vixis / angularplasmid](https://github.com/vixis/angularplasmid), License: _MIT_) by Rehan Chawdry is an AngularJS library for biological plasmid visualisation:

> Rather than coding client-side JavaScript or other server-side programming languages, AngularPlasmid provides easy-to-use HTML markup, making plasmid generation as easy as creating a web page. In fact, you don't really neeed to know anything about AngularJS or JavaScript to use the components, as one of the download options bundles everything together for you.

[The basic tutorial](http://angularplasmid.vixis.com/usage-basic.php) explains how to create a visualisation using markup rather than having to write JavaScript, so it should appeal to biologists who want to create rich HTML documents that aren't programmers.  In fact, Angular seems like a good choice for this type of visualisation in that you can use it declaratively.
