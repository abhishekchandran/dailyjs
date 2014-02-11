---
layout: post
title: "jQuery UI 1.10.4, jqModal, floatThead"
author: Alex Young
categories:
- jquery
- plugins
- ui
---

###jQuery UI 1.10.4

[jQuery UI 1.10.4](http://blog.jqueryui.com/2014/01/jquery-ui-1-10-4/) is out:

> The fourth maintenance release for jQuery UI 1.10 is out. This update brings bug fixes for Widget Factory, Position, Droppable, Resizable, Accordion, Autocomplete, Button, Datepicker, Dialog, Menu, Slider, Spinner, Tabs, and the CSS Framework. For the full list of changes, see the [changelog](http://jqueryui.com/changelog/1.10.4/).

jQuery UI 1.10.3 was released last May, so it's been quite a while since the last release!

###jqModal

[jqModal](http://jquery.iceburg.net/jqModal/) (GitHub: [briceburg / jqModal](https://github.com/briceburg/jqModal), License: _MIT, GPL_) by Brice Burgess is a plugin for showing modals, popups, and notices.  To use it, you just need a suitable container element with dialog content and then to call `$('#dialog').jqm();`.

It can load content using Ajax, and allows dialogs to be nested.  External content can also be loaded using iframes.

###jquery.floatThead

[jquery.floatThead](https://github.com/mkoryak/floatThead) (GitHub: [mkoryak / floatThead](https://github.com/mkoryak/floatThead/), License: _CC BY-SA 4.0_) by Misha Koryak is a plugin for floating table headers.  Headers can be floated inside elements with overflow scrolling, and also for the entire window.

Overflow scrolling requires that the "scroll container" is specified:

{% highlight javascript %}
var $table = $('table.demo');
$table.floatThead({
  scrollContainer: function($table){
  return $table.closest('.wrapper');
}});
{% endhighlight %}

