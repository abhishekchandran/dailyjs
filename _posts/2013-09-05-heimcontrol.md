---
layout: post
title: "Home Automation with Node"
author: "Alex Young"
categories: 
- node
- modules
- hardware
---

<div class="image">
  <img src="/images/posts/heimcontrol.png" alt="" />
  <small>Heimcontrol to Major Tom...</small>
</div>

I don't post much about hardware on DailyJS, but I really should!  I like tinkering with Arduino and small board computers like the Raspberry Pi -- so far I've managed to use one as a cheap NAS, an IR control (by wiring up an IR sensor to the GPIO pins), and a [96khz/24bit audio player](http://hifimediy.com/index.php?route=product/product&product_id=83).  Naturally I was interested when I saw the [heimcontrol.js project](http://ni-c.github.io/heimcontrol.js/) (GitHub: [ni-c / heimcontrol.js](https://github.com/ni-c/heimcontrol.js), License: _MIT_) by Willi Thiel.

It's currently being debated on [Hacker News](https://news.ycombinator.com/item?id=6333838), but hasn't been updated for five months -- hopefully the publicity will get people contributing to the project.  It uses an Arduino board with the Pi, and provides access to the GPIO pins so you can communicate with both analogue and digital systems.

There's a video on the project page that shows the HTML/WebSocket/MongoDB-based interface in use.  The user is able to view and change a temperature control, turn a radio light switch on and off, and also operate a TV by IR through the Arduino board.

The user interface is responsive, so it looks good on a desktop or phone.  If you get this running and have USB ports spare, you could always add some other stuff to it like [ASIC miners](http://learn.adafruit.com/piminer-raspberry-pi-bitcoin-miner/initial-setup-and-assembly)!
