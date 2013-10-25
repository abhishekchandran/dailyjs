---
layout: post
title: "How Apple Could Fix iWork: JavaScript"
author: "Alex Young"
categories: 
- apple
- essays
- embedding
---

![Apple and JavaScript](/images/posts/jsapple.png)

Apple recently updated iWork and removed a whole bunch of features.  The company where I work makes a popular Mac application, and the removal of AppleScript from iWork caused a backlash from customers who rely on this feature for integration between our program, and Pages and Numbers.

AppleScript wasn't ideal, but it did the job.  Now we're left in the dark, and as Apple are being typically opaque about adding it back we're not sure what to do.  The way it worked before was with [scripting bridge](https://developer.apple.com/library/mac/documentation/Cocoa/Reference/SBApplication_Class/SBApplication/SBApplication.html), and although `SBApplication` is still around, Pages and Numbers no longer have it.

###Scripting Bridge

Scripting Bridge provides an Objective-C API for sending and receiving Apple events, so you can take control of applications in Objective-C.  It can be used to bridge another scripting language.  [JSTalk](http://jstalk.org/) is one such example:

> JSTalk is a scripting language for Mac OS X built on top of JavaScript, with a bridge to Apple's Cocoa libraries. You can use it to communicate with other applications just like AppleScript does

> JSTalk is built on top of Apple's JavaScriptCore, the same JavaScript engine that powers Safari. So when you write in JSTalk, you are really writing JavaScript.

There's also [JavaScript Bindings for C and Objective-C](https://github.com/zynga/jsbindings).  This uses SpiderMonkey to interpret your JavaScript, and bindings for Objective-C.  You can even subclass native objects with JavaScript.

From my perspective as a JavaScript and Node specialist who does some Objective-C on the side, these projects have their appeal.  It would be better if JavaScript was the default, though.

###JavaScriptCore

Apple makes JavaScriptCore available to Mac and iOS developers with an Objective-C API.  This quote is from [Owen Mathews at Big Nerd Ranch](http://blog.bignerdranch.com/3784-javascriptcore-and-ios-7/):

> JavaScriptCore gives developers deep access to the full JavaScript runtime from Objective-C. You can syntax-check and execute scripts, access variables, receive callbacks, and share Objective-C objects, making possible a wide range of interactions. (One caveat: on iOS, there is currently no way to access the UIWebView’s runtime, so unfortunately it’s not possible to tie into web apps at this level.)

###Post Scripting Bridge

Now Apple have removed Scripting Bridge from iWork, it made me want to rethink application scripting.  What would it be like to run JavaScript in an application?  It would be much like browser DOM scripting, except the document would be a Keynote or Pages file.

When we wrote AppleScript in the past we wanted to modify a document without having to understand how to parse its format.  There's an element of driving the application, but also handling an abstracted version of the document rather than the underlying proprietary format.  It's probably easier to say "make words that match this regular expression bold" than it is to write a parser for Pages documents.

I recently wrote about the importance of [embedded JavaScript](http://dailyjs.com/2013/08/26/embeddedjs/), and I think Apple could gain a lot by adding JavaScript APIs to their applications.  It would be more agnostic than AppleScript or VBScript, which can be used with Microsoft Office.  If I could somehow insert myself into the nexus of all Apple development and advocate JavaScript I would, but I don't have that kind of power, so perhaps someone reading this will!
