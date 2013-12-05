---
layout: post
title: "Multiprocess Firefox"
author: "Alex Young"
categories: 
- firefox
- browsers
---

![Multiprocess Firefox](/images/posts/firefox-multi.png)

I know a lot of DailyJS readers who use Chrome and Safari as their main browsers, partly due to iOS and Android's popularity, and partly because Chrome's initial performance gains enticed them away from Firefox.  The big issue over the last few years has been the fact browsers are switching to using multiple processes, the idea being that resources can be shared better and fallout from crashes can be mitigated.

If Firefox isn't your main browser, you probably use it for testing or just try it out every few months to see what's been going on.  The thing most of us have been looking for is Chrome (and apparently IE)-style multi-process support.  Bill McCloskey has written a post about this very topic: [Multiprocess Firefox](http://billmccloskey.wordpress.com/2013/12/05/multiprocess-firefox/).  Bill is a programmer at Mozilla, and you may remember his post about [incremental GC in Firefox](https://blog.mozilla.org/javascript/2012/08/28/incremental-gc-in-firefox-16/).

Although the work so far sounds promising, there are some major technical hurdles.  These partly relate to the nature of how JavaScript interacts with the DOM, and how Firefox handles add-ons:

> JavaScript execution and layout happen on the main thread, and they block the event loop. Running these components on a separate thread is difficult because they access data, like the DOM, that are not thread-safe. As an alternative, we've considered allowing the event loop to run in the middle of JavaScript execution, but doing so would break a lot of assumptions made by other parts of Firefox (not to mention add-ons).

> Like the threaded approach, Firefox is able to run its event loop while JavaScript and layout are running in a content process. But unlike threading, the UI code has no access to content DOM or other content data structures, so there is no need for locking or thread-safety. The downside, of course, is that any code in the Firefox UI process that needs to access content data must do so explicitly through message passing.

You might not realise it, but Firefox itself uses a lot of JavaScript:

> Content scripts. [IPDL](https://wiki.mozilla.org/IPDL) takes care of passing messages in C++, but much of Firefox is actually written in JavaScript. Instead of using IPDL directly, JavaScript code relies on the message manager to communicate between processes.

> We decided to do the message passing in JavaScript instead, since it's easier and faster to prototype things there. Rather than change every docshell-using accessor to test if we're using multiprocess browsing, we decided to create a new XBL binding that applies only to remote `<browser>` elements. It is called remote-browser.xml, and it extends the existing browser.xml binding.

If you're an add-on author, you'll be pleased to hear add-ons are being taken seriously.  However, Mozilla may need your help in the future:

> We realize that add-ons are extremely important to Firefox users, and we have no intention of abandoning or disrupting add-ons. At the same time, we feel strongly that users will appreciate the security and responsiveness benefits of multiprocess Firefox, so we're willing to work very hard to get add-ons on board. We're very interested in working with add-on developers to ensure that their add-ons work well in multiprocess Firefox.

It's hard to imagine Firefox OS not using multiple processes, and Bill mentions this early on in the post:

> Firefox OS relies heavily on the multiprocessing and IPC code introduced during Electrolysis.

[Electrolysis](https://wiki.mozilla.org/Electrolysis) was a project to use multiple processes, but the focus was tighter than changing the desktop browser.  Firefox's layout engine, Gecko, supports multiple threads, and the "Gecko platform" supports multiple processes.  But, as the Electrolysis wiki page points out, the Firefox frontend does not currently use multiple processes.

Will we see a browser share increase when Firefox is updated to support multiple processes?  I don't know, but as a front-end developer I'm excited about seeing this feature released sooner rather than later.
