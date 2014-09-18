---
layout: post
title: "JavaScript for Automation in Yosemite"
author: "Alex Young"
categories:
- apple
- scripting
---

I seem to remember that I once wrote on DailyJS about how Apple should start using JavaScript instead of AppleScript, and the possibility of cross-platform scripting with JavaScript.  It looks like this is finally happening in Yosemite, highlighted in Apple's [JavaScript for Automation](https://developer.apple.com/library/prerelease/mac/releasenotes/InterapplicationCommunication/RN-JavaScriptForAutomation/index.html) documentation (and [HN](https://news.ycombinator.com/item?id=8328760)).

What does it look like?  Here's a sample for Mail:

{% highlight javascript %}
var Mail = Application('Mail');

var message = Mail.OutgoingMessage({
  subject: 'Hello world',
  visible: true
});

Mail.outgoingMessages.push(message);
{% endhighlight %}

It goes further, though, with the Objective-C bridge:

> JavaScript for Automation has a built-in Objective-C bridge that offers powerful utility such as accessing the file system and building Cocoa applications.
>
> The primary access points for the Objective-C bridge are the global properties `ObjC` and `$`.

There are mappings for Objective-C methods and data types, and you can load frameworks that are built with bridge support using `ObjC.import`.

This bridge layer should make it possible to build native Cocoa applications that are partly drive by JavaScript, allowing you to potentially centralise some business logic into JavaScript that can run in Apple's environment or the equivalent for .NET.

This is made possible thanks to the design of the [Open Scripting Architecture](https://developer.apple.com/library/mac/documentation/applescript/conceptual/applescriptx/concepts/osa.html), and JavaScript is the second language after AppleScript that has been added.

On the commercial project I work on our [Mac team recently tested JavaScript](http://blog.papersapp.com/scripting-papers/) support for our scripting API.  It's definitely going to make it easier for me to automate things!
