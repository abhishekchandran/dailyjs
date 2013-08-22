---
layout: post
title: "Debugging with Mocha"
author: "Alex Young"
categories: 
- node
- modules
- testing
- techniques
---

I do a lot of work with [Mocha](http://visionmedia.github.io/mocha/), because I like to write well-tested Node projects.  Sometimes there are things I just can't figure out non-interactively, and that's when I reach for the debugger.  It's a lot better than repeatedly running tests with more and more `console.log` statements.

Rather than using any extra Mocha extensions, I find Node's standard debugger works great.  With Mocha you access it by running your tests in debug mode:

{% highlight text %}
mocha debug
{% endhighlight %}

The `debug` option works just like `node debug file.js`.  [Node's debugger](http://nodejs.org/api/debugger.html) comes from [V8](https://code.google.com/p/v8/wiki/DebuggerProtocol), which has a built-in JSON-based protocol that supports communication with a live process using TCP.  That means you're not limited to Node's command-line tools: the [fancy GUI debugger in Chrome can be used](https://github.com/node-inspector/node-inspector) instead.

###Debugging a Failing Test

To debug a failing test, look at the stack trace to figure out a good place to add a breakpoint.  I usually put them in test cases, just before a failing assertion, but you can put them anywhere in the program.

Breakpoints are added by inserting `debugger` on a single line by itself.  Once you've strategically placed some breakpoints, run the tests with `mocha debug`.

Whenever you run `mocha debug` or `node debug`, you'll be dropped into the debugger on the first line of the program.  Type `c` to allow the tests to _continue_ until the first `debugger` statement is encountered -- there may be a delay after you issue the continue command, so be patient.  After that the program will run until a breakpoint is hit, at which point you'll be dropped into a prompt.

###Debugger Commands

The commands are like `gdb` or `lldb` for the most part -- if you've used another debugger before you should be able to figure out what's going on.  If not, there are three main commands that will get you started:

* `s`: Step into code
* `n`: Run the next line without stepping into it if it's a function/method call
* `repl`: Enter a REPL, which we mainly use for printing values and objects

As I have some experience with other debuggers, I found it took me a while to get used to typing `repl`: in most debuggers there's a specific command for printing and formatting values or locations in memory.  This REPL mode is exited by typing `CTRL-C` once.  While you're in the REPL, you can type the name of a value or object to see it: this is usually how I fix most of the problems in my tests.

###Other Thoughts

I haven't found a way to automatically drop into a debugger when an assertion fails.  I'd really like to do this -- it would be a bit like how IDEs work, but I'm not sure if it's possible.
