---
layout: post
title: "jQuery Roundup: QUnit 1.11, Knockout-jQueryUI, Tab Override, FilteredPaste.js"
author: Alex Young
categories:
- jquery
- plugins
- testing
- knockout
- keyboard
- paste
---

<div class="intro">
Note: You can send your plugins and articles in for review through our <a href="/contact.html">contact form</a>.
</div>

###QUnit 1.11

There's a good post on the official jQuery blog about a change in direction to the QUnit project: [QUnit 1.11 Release: A Look Back (and Forth)](http://blog.jquery.com/2013/01/24/qunit-1-11-release-a-look-back-and-forth/).  It discusses some of the history behind QUnit, and includes a [survey](https://docs.google.com/spreadsheet/viewform?formkey=dDBzQl9TWmQzbDdXS08wMTBuLTlObXc6MQ#gid=0) where you can share how you're using it.

###Knockout-jQueryUI

Trying to integrate libraries like [Knockout](http://knockoutjs.com/) is sometimes confusing when you're already using jQuery UI.  To address this, Vas Gábor has created [Knockout-jQueryUI](http://gvas.github.com/knockout-jqueryui/index.html) (GitHub: [gvas / knockout-jqueryui](https://github.com/gvas/knockout-jqueryui), License: _MIT_), which is a collection of Knockout bindings for jQuery UI widgets.

It's small, comes with a build script and unit tests, and the author has provided full documentation on the project's homepage.

###Tab Override

[Tab Override](https://github.com/wjbryant/taboverride) (GitHub: [wjbryant / taboverride](https://github.com/wjbryant/taboverride), License: _MIT_, bower: _taboverride_) by Bill Bryant allows the tab key to insert tabs in `textarea` elements.  It also supports auto indent and multi-line tab insertion.

There's also a [jQuery Tab Override plugin](https://github.com/wjbryant/jquery.taboverride), and both scripts are AMD-compatible.  Bill has included QUnit tests, which actually simulate key presses to test the script's various features.

###FilteredPaste.js

[FilteredPaste.js](http://willemmulder.github.com/FilteredPaste.js/) (GitHub: [willemmulder / FilteredPaste.js](https://github.com/willemmulder/FilteredPaste.js), License: _CC BY-SA 3.0_) by Willem Mulder can be used to filter text when it's pasted into `textarea` elements, or anything with the `contenteditable` attribute.  Why is this useful?  Well, Willem got tired of dealing with support requests when text pasted from Word into his CMS carried across unwanted formatting.

I find myself always using _Paste and Match Style_ and wondering why this isn't the default for the paste keyboard shortcut.  The only time I've ever wanted to include formatting when pasting is when I make slides in Keynote/PowerPoint/Google Drive and want to include syntax highlighting in my examples.  And that seems like an edge case if ever there was one!

