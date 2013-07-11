---
layout: post
title: "Review: Kodiak JavaScript"
author: Alex Young
categories:
- apps
- iOS
- reviews
---

[Kodiak JavaScript](http://www.becomekodiak.com/kodiak-javascript.html) (iTunes: [Kodiak JavaScript](https://itunes.apple.com/app/kodiak-javascript/id658323781?mt=8), Price: $4.99) is an iOS IDE created by [@becomekodiak](https://twitter.com/becomekodiak), a group of developers that apparently really like bears.

<div class="image">
  <img alt="" src="/images/posts/kodiak-header.png" />
  <small>Kodiak's file browser and editor views, and the sidebar.</small>
</div>

This app comes bundled with over 50 libraries and frameworks familiar to JavaScript developers, and most of the features you might expect: syntax highlighting with various themes, a tabbed editor, a file navigator, and a preview mode that uses the built-in WebKit browser.  It also supports Retina displays and external keyboards.

The settings panel allows the theme, font, and font size to be changed.  I found DejaVuSansMono looked best.  A preview is displayed in the same view so you can easily see what each option does.

<div class="image">
  <img alt="" src="/images/posts/kodiak-body.png" />
  <small>The IDE settings and the impress.js demo being previewed.</small>
</div>

I tried it out with some of the bundled libraries -- [impress.js](http://bartaz.github.io/impress.js/) for example worked fine, and I made a quick scratch project just to get a feel for the basics.

One of the best features in the app is the keyboard.  Much like other text or terminal apps, it includes a bar with commonly used keys along the top.  It has a button in the centre which can be used to move the cursor around easily, and the other keys have gesture-based punctuation shortcuts which are great for quickly inserting quotes and brackets.

Kodiak doesn't like loading large files which I suspect is a limitation of their editor design -- for your own files it should be fine, but if you try to open a 40 KB JavaScript library it'll make the device slow down quite a bit.  Also, large files can't be edited, they open in a read-only mode instead.

I don't remember [VimTouch](https://play.google.com/store/apps/details?id=net.momodalo.app.vimtouch.fullruntime) having limitations like that, but it's a very different application.  In fact, I think the strength of Kodiak JavaScript lies in its educational value -- if you're starting out learning JavaScript it could be a great companion application to a suitable Kindle/iBooks eBook.

I noticed that one of the Kodiak developers has a GitHub account with some polished-looking Objective-C projects: [Adam Horacek](https://github.com/adamhoracek/).  This includes the cool keyboard found in the Kodiak apps, which is [KOKeyboard](https://github.com/adamhoracek/KOKeyboard).  Adam's work is definitely worth taking a look at if you do any iOS development.
