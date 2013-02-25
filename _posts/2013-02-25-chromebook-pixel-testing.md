---
layout: post
title: "Mobile Testing on the Chromebook Pixel"
author: Alex Young
categories: 
- testing
- laptops
- touchscreen
- mobile
---

<p></p>
<div class="image">
  <img src="/images/posts/chromebook-pixel.png" alt="" />
  <small>The Pixel.</small>
</div>

Last week I was invited to a "secret workshop" at one of the Google campuses in London.  Knowing that [Addy Osmani](http://addyosmani.com/blog/) works there I expected something to do with Yeoman or AngularJS, but it turned out to be a small launch event for the Chromebook Pixel.  I ended up walking out of there with my very own Pixel -- no, I didn't slip one into my backpack and run off wearing a balaclava, each attendee was given one to test.

Looking at this slick metallic slab of Google-designed hardware I was left wondering what to do with it as a JavaScript hacker.  It runs Chrome OS and has a high density multi-touch display.  That made me wonder: how useful is the Pixel as a multi-touch, "retina" testing device?  My personal workflow for client-side development is to preview sites on my desktop or laptop, then switch to testing with mobile devices towards the end of the project.  I may occasionally have a tablet or phone close by for experimental work or feasibility studies, but generally I leave the device testing until later.

By using a Pixel early in development the potential is there to work "touch natively" -- focusing on touch as a primary input mode rather than a secondary option.

If you're working on mobile sites, responsive designs, or browser-based games, then how well does the Pixel function as a testing machine?  With one device you get several features that are useful for testing these kinds of sites:

1. The touchscreen.  Rather than struggling with a tablet or phone during early development you get a touchscreen _and_ the standard inputs we're more used to.
2. The screen's high resolution is useful for testing sites that optionally support high density displays.
3. Chrome's developer tools make it easy to override the browser's reported size and user agent which is useful for testing mobile and responsive designs.

I've been using the Pixel with several mobile frameworks and well-known mobile-friendly sites to see how well these points play out in practice.

###Testing Mobile Sites with Chrome

Pressing `ctrl-shift-j` opens the JavaScript console on a Chromebook.  Once you're in there, selecting the settings icon opens up some options that can be used to simulate a mobile browser.  The 'Overrides' tab has a user agent switcher which has some useful built-in browsers like Firefox Mobile and Android 4.x.  There's also an option for changing the resolution, which changes the resolution reported to the DOM rather than resizing the window.

###The Screen and Multi-Touch

The screen itself is 2560x1700 and 3:2 (239 ppi).  It's sharp, far better than my battle-worn last gen MacBook Air.  One of the Google employees at the event said the unusual aspect ratio was because websites are usually tall rather than wide, so they optimised for that.  In practice I haven't noticed it -- the high pixels per inch is the most significant thing about it.

I tried [Multitouch Test](http://openlayers.org/dev/examples/multitouch.html) and it was able to see 10 unique points -- I'm not sure what the limit is and I can't find it documented in Google's technical specs for the Pixel.

###The Touchpad

This article isn't intended to be a review of the Pixel.  However, I really love the touchpad.  I've struggled with non-Apple trackpads on laptops before, but the Pixel's touchpad is accurate and ignores accidental touches fairly well.  The click action feels right -- it doesn't take too much pressure but has a satisfying click.  I also like the soft finish, which makes it feel comfortable to use even with my sweaty hands.

###Testing Mobile Frameworks

I tested some well-known mobile frameworks and sites purely using the touchscreen.  I set Chrome to send the Android browser user agent, and I also tried Chrome for Android and Firefox Mobile.

The Google employees at the event were quick to point out that _everything_ works using touch.  It seems like a lot of effort has been put into translating touches into events that allow UI elements to behave as expected.

That made me wonder if sites optimised for other touch devices would fail to interpret touch events and gestures on the Pixel -- perhaps reading them as mouse events instead -- but all of the widgets and gestures I tried seemed to work as intended.  I even ran the touch event reporting in Enyo and Sencha Touch to confirm the gestures were being reported correctly.

During the event, I opened The Verge on my phone just to check what the press was saying about the Pixel.  There was mention of touchscreen interface lag, and Gruber picked this up on [Daring Fireball](http://daringfireball.net/linked/2013/02/21/chromebook-pixel).  I don't have any way of measuring the lag [scientifically](http://citeseerx.ist.psu.edu/viewdoc/summary?doi=10.1.1.187.641) myself (I hope to see a [Digital Foundry](http://www.eurogamer.net/?topic=df-hardware)-style analysis of the device), but in practice it feels like a modern tablet so I haven't had a problem with it.  I'm not sure where Gruber gets "janky" from, but as the Pixel will be sold in high street stores across the UK and US you should be able to try it out in person.

jQuery Mobile worked using the touchscreen for standard navigation, and also recognised swipes and dragging.

<div class="image">
  <img src="/images/posts/pixel-jquery-mobile.png" alt="" />
  <small>jQuery Mobile's widgets worked with touch-based gestures.</small>
</div>

Enyo also seemed to recognise the expected gestures.

<div class="image">
  <img src="/images/posts/pixel-enyo-gestures.png" alt="" />
  <small>Enyo worked as it would on a touchscreen phone or tablet.</small>
</div>

The Sencha Touch demos behaved as they would on a mobile device.

<div class="image">
  <img src="/images/posts/pixel-sencha-touch.png" alt="" />
  <small>Sencha Touch, showing the event viewer.</small>
</div>

Bootstrap's responsive design seemed to cope with different sizes and touch gestures.

<div class="image">
  <img src="/images/posts/pixel-bootstrap.png" alt="" />
  <small>Bootstrap on the Pixel.</small>
</div>

###Testing Mobile Sites

<div class="image">
  <img src="/images/posts/pixel-guardian.png" alt="" />
  <small>The Guardian's mobile site running on the Pixel.</small>
</div>

I tested some sites that I know work well on mobile devices, and used the touchscreen to interact with them.  Again, this was with Chrome's user agent changed to several mobile browsers.

* [2560x1700: BBC Weather](/images/posts/pixel-bbc-weather.png)
* [2560x1700: Engadget](/images/posts/pixel-engadget.png)
* [2560x1700: Mashable](/images/posts/pixel-mashable.png)
* [2560x1700: Twitter](/images/posts/pixel-twitter.png)

###Development Test

The way I write both client-side projects and server-side code is with Vim, tmux, and command-line tools.  This doesn't translate well to Chrome OS -- it can be done by switching the machine into developer mode, but this requires some Linux experience.  The Pixel supports dual booting, and [Crouton](https://github.com/dnschneid/crouton) seems worth checking out if you're a Chromebook user.

I wrote this article primarily for client-side developers, so I imagine you'd prefer to use the OS as it was intended rather than installing Linux.  With that in mind, I tried making some small projects using jQuery Mobile and [Cloud9 IDE](https://c9.io/).  Cloud9 worked well for the most part -- I had the occasional crashed tab, but I managed to get a project running.

<div class="image">
  <img src="/images/posts/pixel-c9.png" alt="" />
  <small>Cloud9 IDE with its HTML preview panel.</small>
</div>

One quirk I found was I used the jQuery Mobile CDN assets served using HTTP, whereas Cloud9 is always served over SSL.  When I tried to preview my HTML files the CDN assets were blocked by Chrome, and only a small shield icon in the address bar indicated this so it wasn't immediately obvious.

Also, Cloud9 might not fit into your existing workflow.  While it supports GitHub, Bitbucket, SSH, and FTP, it takes a bit of effort to get an existing project running with it.

If you were sold on using the Pixel as a high DPI touchscreen testing device, then the fact you can at least get some kind of JavaScript-friendly development going is useful.  However, prepare to make some compromises.

###Other Notes

Chrome syncs _quickly_.  Try signing in with Chrome on multiple computers and installing apps or changing themes to see what I mean.  The upshot of this is the Chromebook is reliable when syncing with Google's services.  You lose this somewhat with other services depending on how they're built.  Cloud9 IDE, for example, has an offline mode, but I haven't tested it well enough to see how resilient it is at syncing the data back again.

Switching accounts on a Chromebook isn't much fun.  Chrome OS doesn't support anything like fast user switching, and I use a ridiculously long password stored in a password manager, so I'll do anything to avoid typing it in.  Also, 1Password doesn't have an extension for Chrome OS -- you can use the HTML version (1Password Anywhere), but that is limited and isn't particularly friendly.  Last Pass works though.

###Conclusion

I love the look of the Pixel, it exudes luxury, and the OS is incredibly low maintenance.  As for a mobile development testing rig -- it does the job, but you may find [Chrome's remote debugging tools](https://developers.google.com/chrome-developer-tools/docs/remote-debugging) and a cheap tablet to work well enough.  Being able to dip into Chrome's developer tools on a local device and use a keyboard and mouse is natural and convenient: it makes mobile testing feel like cheating!

Chromebooks are designed to sync constantly, which means you technically don't have to worry about losing data if yours gets damaged or stolen.  As it stands it's a trade-off: you lose the ability to install your standard development tools but gain a lower maintenance and potentially more secure OS.

While I respect Cloud9 IDE, I feel like there are people clamouring for a product close to the Pixel that better supports developers.  Perhaps [Native Client](https://code.google.com/p/nativeclient/) will make this possible.  We are the ultimate early adopters, so sell us machines we can code on with our preferred tools!

