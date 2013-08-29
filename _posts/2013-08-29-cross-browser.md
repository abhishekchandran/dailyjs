---
layout: post
title: "Dropping Legacy IE Is No Panacea"
author: "Alex Young"
categories: 
- browser
- ie
- dojo
- chrome
---

The presiding sentiment of client-side developers seems to be that dropping legacy IE support fixes cross-browser issues.  While it does reduce a lot of rendering quirks, it doesn't mean you can stop browser testing altogether.

The reality is that there are four popular browsers with a wide range of versions.  Using DailyJS's readership during August as an example, Chrome's versions break down like this: Chrome 28 has 53%, and Chrome 29 is at 13%.  Firefox has 43% on version 22 and 41% on version 23.  That means we see very few Firefox and Chrome readers on older versions, so they're doing an excellent job of keeping users up to date.  Digging into the IE stats, I can see 50% using IE 10, and 0.33% on IE 6!

Why am I bothering you with browser stats?  It was because I saw this bug in Dojo earlier today: [#17400: Chrome 29 breaks dojo.query in Dojo 1.4.4 through Dojo 1.6](https://bugs.dojotoolkit.org/ticket/17400).  The Dojo developers quickly [fixed the bug](https://github.com/dojo/dojo/commit/fc262d0d589c490cdd671791f1546a4665ed69c6).  It seems someone had used array-style accessors on a DOM node instead of the `children` and `childNodes` properties.

Even though IE 10 is far better than its predecessors, and Chrome and Firefox see fast upgrade rates due to their update mechanisms, you can't leave out proper cross-browser testing.  It's hard work and dull, but unfortunately still important.  I have a feeling the disparity in mobile browser technology will be the new IE 6, but that's another story...
