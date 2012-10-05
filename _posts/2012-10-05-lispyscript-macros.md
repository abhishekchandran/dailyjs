---
layout: post
title: "Tutorial: Writing LispyScript Macros"
author: Santosh Rajan
categories:
- LispyScript
- tutorials
- lisp
---

<div class="box">
  This tutorial is by Santosh Rajan (<a href="https://twitter.com/santoshrajan">@santoshrajan</a>), the creator of <a href="http://lispyscript.com/">LispyScript</a> (GitHub: <a href="https://github.com/santoshrajan/lispyscript">santoshrajan / lispyscript</a>).
</div>

###Writing LispyScript Macros

Macros are a powerful feature of LispyScript. They are much more powerful than C `#define` macros. While C `#define` macros do string substitution, LispyScript macros are _code generators_.

Functions take values as arguments and return a value. Macros take code as arguments, and then return code. Understanding this difference and its ramifications is the key to writing proper macros.

Functions get evaluated at runtime. Macros get evaluated at compile time, or pre-compile time to be more precise.

So, when should macros be used? When you cannot use a function! There is more to this answer than what is apparent. Consider this piece of code:

{% highlight text %}
(* 2 2)
{% endhighlight %}

And elsewhere in the program we find this.

{% highlight text %}
(* 4 4)
{% endhighlight %}

There is a pattern emerging here. In both cases we have the same code `*`, and a variable -- a number that changes in each instance of the pattern. So we reuse this pattern by writing a function:

{% highlight text %}
(var square
  (function (x)
    (* x x)))
{% endhighlight %}

Therefore, to reuse a repeating code pattern as a function, the code pattern must meet two conditions:

1. The code must remain the same across every instance of the code pattern.
2. It is only the data that can change across every instance of the code pattern.

Using functions to reuse repeated code patterns has its limitations. You cannot use a function if it is the code part that changes in a repeated code pattern.

Consider the two functions below (str is an expression that adds up given strings):

{% highlight text %}
(var greet
  (function (username)
    (str "Welcome " username)))

(var link
  (function (href text)
    (str "<a href=\"" href "\">" text "</a>")))
{% endhighlight %}

There is a repeating code pattern here. Given below is the pattern with the parts that change in capitals:

{% highlight text %}
(var NAME
  (function ARGUMENTS
    (str TEMPLATE_STRINGS)))
{% endhighlight %}

We cannot use a function to reuse this code pattern, because the parts that change are parts of the code.

Functions are about reusing code patterns, where it is only the data that changes.

Macros are about reusing code patterns, where the code can also change.

In LispyScript, we can write a macro to reuse this code pattern. The macro needs a name, let's call it `template` as it happens to be a template compiler:

{% highlight text %}
(macro template (name arguments rest...)
  (var ~name
    (function ~arguments
      (str ~rest...))))
{% endhighlight %}

Now compare this with the meta code pattern in the previous example. The arguments to this macro are the parts of the code that change -- `NAME`, `ARGUMENTS`, `TEMPLATE_STRINGS` -- these correspond to `name`, `arguments` `rest..` in the macro definition.

Arguments can be dereferenced in the generated code by adding a `~` to the argument name. `rest...` is a special argument that represents the rest of the arguments to the macro after the named arguments.

This macro can be used by making a call to `template`:

{% highlight text %}
(template link (href text) "<a href=\"" href "\">" text "</a>")
{% endhighlight %}

This code will expand as follows:

{% highlight text %}
(var link
  (function (href text)
    (str "<a href=\"" href "\">" text "</a>")))
{% endhighlight %}

This expansion happens just before the expanded code is compiled. This is known as the _macro expansion phase_ of the compiler.

Now let's try another example. We will write a benchmark macro, which benchmarks a line of code. But first we'll write a benchmark function to get a couple of related issues out of the way.

{% highlight text %}
(var benchmark
  (function ()
    (var start (new Date))
    (+ 1 1)
    (var end (new Date))
    (console.log (- end start))))
{% endhighlight %}

This is not an example that always works. Because JavaScript can only resolve time up to milliseconds, but to benchmark an integer `+` operation we need a resolution down to nanoseconds.

Furthermore, the function does not scale. We need to benchmark various operations and expressions, and since this involves changes to the above code we need to write a macro. In the macro we print the result of the operation along with the elapsed time:

{% highlight text %}
(macro benchmark (code)
  (do
    (var start (new Date))
    (var result ~code)
    (var end (new Date))
    (console.log "Result: %d, Elapsed: %d" result (- end start)))
{% endhighlight %}

It can be used like this:

{% highlight text %}
(var a 1)
(var b 2)
(benchmark (+ a b))
{% endhighlight %}

The result printed to the console should look like the following:

{% highlight text %}
Result: 3, Elapsed: 0
{% endhighlight %}

Elapsed is `0` due to the millisecond resolution, but the example seems to run correctly... until one day someone attempts to do this:

{% highlight text %}
(var start 1)
(var b 2)
(benchmark (+ start b))
{% endhighlight %}

Running this gives confusing results:

{% highlight text %}
Result: NaN, Elapsed: 1
{% endhighlight %}

The result is `NaN`, so something has gone wrong since `3` was expected.  To figure out what's going on, let's look at the macro expansion:

{% highlight text %}
(var start 1)
(var b 2)
(do
  (var start (new Date))
  (var result (+ start b))
  (var end (new Date))
  (console.log "Result: %d, Elapsed: %d" result (- end start))
{% endhighlight %}

The user has created a variable `start`. It so happens that the macro also creates a variable called `start`. The macro argument `code` gets dereferenced in the new scope. When `(+ start b)` got executed the `start` variable used was the `start` _Date_ variable created in the macro code. This problem is known as __variable capture__.

When writing macros, you have to be very careful when creating a variable inside a macro. In our `template` macro example we were not concerned about this problem, because the `template` macro does not create its own variables.

In LispyScript we get around this problem by following two rules which are specified in the "guidelines" section of the document:

1. When writing a LispyScript program, creating a variable name that starts with three underscores is NOT allowed, for example: `___varname`.
2. When writing a macro you MUST start a variable name with three underscores if you want to avoid variable capture. There are cases where you want variable capture to happen, in which case you do not need to use the three underscores. For example, when you want the passed code to use a variable defined in the macro.

The benchmark macro should be refactored using three underscores:

{% highlight text %}
(macro benchmark (code)
  (do
    (var ___start (new Date))
    (var ___result ~code)
    (var ___end (new Date))
    (console.log "Result: %d, Elapsed: %d" ___result (- ___end ___start)))
{% endhighlight %}

###Conclusion

Macros are a very powerful feature of LispyScript. It allows you to do some nifty programming, which is otherwise not possible with functions. At the same time we have to be very careful when using macros.  Following the LispyScript macro guidelines will ensure your macros behave as expected.
