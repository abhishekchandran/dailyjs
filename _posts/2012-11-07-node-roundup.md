---
layout: post
title: "Node Roundup: Fastworks.js, Probability.js, Colony"
author: "Alex Young"
categories: 
- node
- modules
- visualisation
- statistics
- probability
- games
- frameworks
---

<div class="intro">
You can send in your Node projects for review through our <a href="/contact.html">contact form</a> or <a href="http://twitter.com/dailyjs">@dailyjs</a>.
</div>

###Fastworks.js

[Fastworks.js](https://github.com/RobeeeJay/Fastworks.js) (License: _GPL3_, npm: [fastworks](https://npmjs.org/package/fastworks)) by Robee Shepherd is an alternative to [Connect](http://www.senchalabs.org/connect/).  It includes "stacks" for organising middleware, and middleware for routing, static files, compression, cookies, query strings, bodies in various formats (including JSON), and a lot more.  It can also work with Connect modules.

The primary motivation for developing Fastworks.js was speed:

> According to the author's benchmarks, it can handle more than twice the requests per second that Connect's Send module can.

That sounds promising, but the author hasn't included benchmarks alongside his project.  It also doesn't include tests.  Hopefully the author will include tests and benchmarks to get this project off the ground.

###Probability.js

![Probability.js](/images/posts/probability-js.png)

[Probability.js](https://github.com/fschaefer/Probability.js) (License: _MIT_) by Florian Schäfer is a fascinating little project that helps call functions based on probabilities.  Functions are paired alongside a probability so they'll only be called some of the time.

That doesn't sound useful on the surface, but the author suggests it could be useful in game development.  Although if you've played the recent XCOM game you may be disillusioned by randomness in games, which is actually quite a well-trodden topic in the games development community.  [Analysis: Games, Randomness And The Problem With Being Human](http://www.gamasutra.com/view/news/34038/Analysis_Games_Randomness_And_The_Problem_With_Being_Human.php#.UJpZKGmopQI) by Mitu Khandaker is an interesting analysis of games and chance.

###Colony

![Colony](/images/posts/colony.png)

[Colony](http://hughsk.github.com/colony/) (GitHub: [hughsk / colony](https://github.com/hughsk/colony), License: _MIT_, npm: [colony](https://npmjs.org/package/colony)) by Hugh Kennedy displays network graphs of links between Node code and its dependencies, using [D3.js](http://d3js.org/).

The network can be navigated around by clicking on files -- the relevant source will be displayed in a panel.  Files are coloured in groups based on dependencies, so it's an intuitive way to navigate complex projects.
