---
layout: post
title: "Node PiGlow"
author: Alex Young
categories:
- node
- modules
- hardware
---

<div class="image">
  <img src="/images/posts/piglow.png" alt="" />
  <small>The PiGlow in action.</small>
</div>

The [PiGlow](http://shop.pimoroni.com/products/piglow) is a small board for the Raspberry Pi that adds 18 single colour LEDs.  Each can be controlled through I2C over the GPIO header, and you can even dim LEDs.

node-piglow (GitHub: [zaphod1984 / node-piglow](https://github.com/zaphod1984/node-piglow), License: _MIT_, npm: [piglow](https://npmjs.org/package/piglow)) by Manuel Ernst is a module for talking to the PiGlow.  It uses [i2c](https://npmjs.org/package/i2c) and allows you to address the LEDs like this:

{% highlight javascript %}
piGlow.l_0_0 = 100; // lights up the first LED in the first LEG with a brightness of 100
piGlow.l_0_0; // lights up the first LED of the first LEG with maximum brightness (255)

piGlow.leg_0 = 100; // lights up the first leg (8 consecutive LEDs) with brightness of 100

piGLow.leg_0; // maximum brightness for the first leg

piGlow.ring_0 = 100; // sets LED 1 of leg 1, LED 1 of leg 2 and LED 1 of leg 3 to 100

iGlow.ring_0; // sets LED 1 of leg 1, LED 1 of leg 1 and LED 1 of leg 2 to 255
{% endhighlight %}

Manuel made [node-piglow-load](https://github.com/zaphod1984/node-piglow-load) with it which uses the PiGlow to visualise system load.  Since the API is very simple you could hook it up to lots of other interesting things, perhaps build status from your next big Node project.  I've had my eye on the PiGlow for a few weeks for fun little hardware projects so I think node-piglow might make me get my wallet out.
