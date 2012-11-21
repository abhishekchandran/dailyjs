---
layout: post
title: "Node Roundup: Knockout Winners, Node for Raspberry Pi, Benchtable"
author: "Alex Young"
categories: 
- node
- raspberry-pi
- hardware
- benchmarking
---

<div class="intro">
You can send in your Node projects for review through our <a href="/contact.html">contact form</a> or <a href="http://twitter.com/dailyjs">@dailyjs</a>.
</div>

###Node.js Knockout Winners Announced

![Disasteroids](/images/posts/disasteroids.png)

[Node.js Knockout](http://nodeknockout.com/) had an outstanding 167 entries this year.  The overall winner was [Disasteroids](http://somethingcoded.nko3.jitsu.com/) by [SomethingCoded](http://nodeknockout.com/teams/somethingcoded).  It's an original take on several arcade classics: imagine a multiplayer version of _Asteroids_ crossed with the shooting mechanics of _Missile Command_, but with projectiles that are affected by gravity.

The other winners are currently listed on the site, but I've reproduced them here to give the entrants more well-earned kudos:

* _Overall Solo_: [HashPay](http://dothejoy.nko3.jitsu.com/) by [DoTheJoy](http://nodeknockout.com/teams/dothejoy)
* _Innovation_: [Node.js Christmas Sweater](http://coalition-for-the-li.nko3.jitsu.com/) by [Coalition for the Liberation of Itinerant Tree-Dwellers](http://nodeknockout.com/teams/coalition-for-the-li)
* _Design_: [Hex](http://public-class.nko3.jitsu.com/) by [Public Class](http://nodeknockout.com/teams/public-class)
* _Utility/Fun_: [Narwhal Knights](http://watermelon-sauce.nko3.jitsu.com/) by [Watermelon Sauce](http://nodeknockout.com/teams/watermelon-sauce)
* _Completeness_: [Asciigram](http://comorichweb.nko3.jitsu.com/) by [comorichweb](http://nodeknockout.com/teams/comorichweb)
* _Popularity_: [Space bridge](http://design-4-quality.nko3.jitsu.com/info) by [Design 4 Quality](http://nodeknockout.com/teams/design-4-quality)

Congratulations to all the winners, and be sure to [browse the rest of the entries](http://nodeknockout.com/entries) for hours of fun!

###Node on Raspberry Pi

![Node Pi](/images/posts/nodepi.png)

If you've got a [Raspberry Pi](http://www.raspberrypi.org/) you probably already know it's possible to run Node on the ARM-based tiny computer.  If not then [Node.js Debian package for ARMv5](http://www.nodejs-news.com/nodejs-tech/nodejs-armv5-debian/) by Vincent Rabah explains how to get Node running with his custom Debian package.

"But the Raspberry Pi is just a cheap computer, what's so great about it?" I hear you cry in the comments.  There's an intrinsic value to the Raspberry Pi Foundation's efforts in making such hardware suitable for school children.  No offence to Microsoft, but in a country where Office was on the curriculum for "IT" we can use any help we can get aiding the next generation of hackers and professional engineers.

###Benchtable

![Benchtable](/images/posts/benchtable.png)

I love the command-line, it's where I write code, DailyJS, notes, email -- colourful text and ancient Unix utilities abound.  But, I also like to fiddle with the way things look.  For example, if I'm writing benchmarks I don't want to just print them out in boring old monochrome text, I want them to look _cool_.

Ivan Zuzak's [Benchtable](https://github.com/izuzak/benchtable) (License: _Apache 2.0_, npm: [benchtable](https://npmjs.org/package/benchtable)) is built for just such a need.  It prints benchmarks in tables, making it a little bit easier to compare values visually.  It's built on [Benchmark.js](https://github.com/bestiejs/benchmark.js), which is one of the most popular benchmarking modules.

The API is based around the `Benchtable` prototype which is based on `Benchmark.Suite`, so it can be dropped into an existing benchmarking suite without too much effort.
