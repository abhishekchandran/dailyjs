---
layout: post
title: "ExcelJS, Material Refresh"
author: Alex Young
image: "/images/posts/material-refresh.gif"
categories:
- animations
- excel
- spreadsheets
- ui
---

###ExcelJS

ExcelJS (GitHub: [guyonroche/exceljs](https://github.com/guyonroche/exceljs), License: _MIT_, npm: [exceljs](http://npmjs.com/package/exceljs)) by Guyon Roche is a module for converting Excel spreadsheets to styles and JSON.  It was created by reverse engineering Excel files into pure JavaScript, so if you look at the source it's surprisingly readable.  Everything is split up into modules, and simple classes are used to model the main entities in Excel documents.

For example, the [cell.js file](https://github.com/guyonroche/exceljs/blob/master/lib/cell.js) defines a `Cell` object that has methods for addressing the cell and manipulating styles.  This is then used to build data types like `StringValue` and `DateValue`.

It can read and write Excel, and it handles functions, links, fonts, borders, alignments, and fills.  Here's the author's example of reading an Excel file:

{% highlight javascript %}
var workbook = new Excel.Workbook();
workbook.xlsx.readFile(filename)
  .then(function() {
    // use workbook
  });

// pipe from stream
var workbook = new Excel.Workbook();
stream.pipe(workbook.xlsx.createInputStream());
{% endhighlight %}

If you're interested in Excel, then also check out [js-xls](https://github.com/SheetJS/js-xls) and [SheetJS](http://sheetjs.com).

###Material Refresh

<img src="/images/posts/material-refresh.gif" style="width: 530px" alt="" />

[Material Refresh](http://lightningtgc.github.io/material-refresh/) (GitHub: [lightningtgc/material-refresh](https://github.com/lightningtgc/material-refresh/), License: _MIT_, npm: [material-refresh](https://www.npmjs.com/package/material-refresh)) by gctang is a Material Design pull/swipe to refresh library.  It has several modes of display: above surface, below surface, and button.

I tried it out on a mobile device and the animations seemed very smooth.  To use the library, set it up by calling `mRefresh` and then `mRefresh.resolve()` to hide the spinner.

