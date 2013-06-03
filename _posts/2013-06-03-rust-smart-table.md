---
layout: post
title: "Angular Smart Table, TurtleScript"
author: "Alex Young"
categories: 
- angular
- rust
- angularjs
- libraries
- education
---

###Smart Table

![Smart Table](/images/posts/smarttable.png)

[Smart Table](http://lorenzofox3.github.io/smart-table-website/) (GitHub: [lorenzofox3 / Smart-Table](https://github.com/lorenzofox3/Smart-Table), License: _MIT_) by Laurent Renard helps quickly render data as tables in AngularJS projects.  It provides the `smart-table` directive which will render a `rowCollection` -- an array that contains objects for each row.  It also supports layouts by specifying the columns with `columnCollection`, data formatting, and sorting.

Smart Table has some more advanced features as well, like styling and inline editing.  Laurent has included API documentation and unit tests.

###TurtleScript

[TurtleScript](http://cscott.net/Projects/TurtleScript/) (GitHub: [cscott / TurtleScript](https://github.com/cscott/turtlescript), License: _GPLv2_) by C. Scott Ananian from One Laptop per Child aims to provide a Logo-like environment for teaching programming.  TurtleScript itself is based on JavaScript, and uses a bytecode compiler/interpreter.

The TurtleScript documentation has a lot more background that explains what it does and how it works.  Meanwhile, Scott has been working on rusty-turtle (GitHub: [cscott / rusty-turtle](https://github.com/cscott/rusty-turtle), License: _GPLv2_).  This is a TurtleScript implementation written in [Rust](http://www.rust-lang.org/).  If you're interested in the Rust language and want to see what a JavaScript parser in Rust might look like, check it out!

> Rusty-turtle is a "native" bytecode interpreter, so it runs the TurtleScript parser and compiler in order to generate bytecode for it to run.

