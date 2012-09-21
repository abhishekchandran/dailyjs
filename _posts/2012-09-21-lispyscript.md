---
layout: post
title: "Tutorial: LispyScript Introduction"
author: Santosh Rajan
categories:
- LispyScript
- tutorials
- lisp
---

<div class="box">
  This tutorial is by Santosh Rajan (<a href="https://twitter.com/santoshrajan">@santoshrajan</a>), the creator of <a href="http://lispyscript.com/">LispyScript</a> (GitHub: <a href="https://github.com/santoshrajan/lispyscript">santoshrajan / lispyscript</a>).
</div>

###Introduction

LispyScript is a tree structured programming language that compiles to JavaScript. A LispyScript program is made up of one or more LispyScript expressions.

{% highlight text %}
(<function> arg1 arg2 arg3 ...)
{% endhighlight %}

A LispyScript expression is made up of an opening parenthesis, a set of elements separated by space characters, and a closing parenthesis. A LispyScript expression is a function call (this is not exactly accurate, but we will see the exceptions to this later).

The first element evaluates to a function. It may be a function reference or an anonymous function. The rest of the elements are the arguments to the function. The expression evaluates to the return value of the function.

{% highlight text %}
(console.log "Hello World!")
{% endhighlight %}

You will notice that we called `console.log`, which happens to be a JavaScript function, directly from LispyScript. You can call all JavaScript functions from LispyScript, even loaded library functions and object methods. `console.log` also works like `printf()`.

{% highlight text %}
(console.log "2 + 2 = %d" (+ 2 2))
{% endhighlight %}

You can have expressions within expressions in LispyScript. Here the expression `(+ 2 2)` is evaluated first, and replaced with its return value `4`. Then the function `console.log` is called with arguments string `2 + 2 = %d` and value `4`.

And this is all there is to the basic structure of a LispyScript program. LispyScript has a tree structure: expressions within expressions. Let's look at a tree structure almost everyone is familiar with: HTML.

{% highlight html %}
<html lang="en">
  <head>
    <title>My Home Page</title>
  </head>
  <body>
    <h1>Welcome to LispyScript</h1>
  </body>
</html>
{% endhighlight %}

This is a LispyScript HTML template that generates the exact same HTML as above:

{% highlight text %}
(html {lang: "en"}
  (head
    (title "My Home Page"))
  (body
    (h1 "Welcome to LispyScript")))
{% endhighlight %}

We will learn how LispyScript HTML templates work later. For now, you can see that LispyScript has a tree structure. This same code structure can also be a data structure in LispyScript. This is known as homoiconicity -- a fancy term for code having a data structure supported in that language.

When a compiler compiles a language like JavaScript, or Java or C, it first parses the source code into a tree structure known as the syntax tree, and then generates the machine/byte code from the syntax tree. If you could manipulate the syntax tree (which you can't in these languages) while compiling, you could actually modify the language itself in ways not possible in the above mentioned languages and most other languages.

In LispyScript your code -- for all practical purposes -- is the syntax tree itself. And since the language is homoiconic, you can treat your code as data, and even modify the syntax tree! This is what macros do.

###Macros

LispyScript does not have a `print` expression like `printf()` or `console.log` in JavaScript. We know that we can call the JavaScript `console.log` from LispyScript. Now if we could somehow transform a `print` expression into a `console.log` expression, we are done!

{% highlight text %}
(macro print (str rest...)
  (console.log ~str ~rest...))

(print "Hello print macro!")
(print "2 + 2 = %d" (+ 2 2))
{% endhighlight %}

This example extends LispyScript by adding a `print` expression to it. The `macro` expression takes the macro name `print` as its first argument, and a list of argument names representing the arguments that will be passed to `print` as the second argument. The last argument to `macro` is a code template that will be expanded at macro expansion time.

Here the `print` expression takes two arguments, the same as `console.log`, and we name the first argument `str`. The second argument `rest...` is a special argument which represents the rest of the arguments to `print`. `rest...` can represent zero or more arguments.

Inside the template expression we dereference the two arguments by adding a `~` to them. So what happens when we use the `print` expression below?

{% highlight text %}
(print "Hello print macro!")
{% endhighlight %}

The LispyScript compiler works in two steps. First it expands any macro expressions in the code. The previous expression will be expanded to:

{% highlight text %}
(console.log "Hello print macro!")
{% endhighlight %}

And then the compiler compiles the above expression to JavaScript

{% highlight text %}
console.log("Hello print macro!");
{% endhighlight %}

The expression:

{% highlight text %}
(print "2 + 2 = %d" (+ 2 2))
{% endhighlight %}

Is expanded to:

{% highlight text %}
(console.log "2 + 2 = %d" (+ 2 2))
{% endhighlight %}

...and compiled to:

{% highlight text %}
console.log("2 + 2 = %d", (2 + 2));
{% endhighlight %}

This is a very simple example and you don't gain much, but it's good enough to illustrate a simple macro. You might wonder why a `print` function can't be used instead of a `print` macro. Let's see what happens when we write a print function instead.

{% highlight text %}
(var print
  (function (data value)
    (console.log data value)))

(print "2 + 2 = %d" (+ 2 2))
{% endhighlight %}

This will work too, but have a look at the compiled output:

{% highlight text %}
var print = function(data,value) {
    return console.log(data,value);
};
print("2 + 2 = %d",(2 + 2));
{% endhighlight %}

The print function must be included alongside the _call_ to it in the compiled output! When we used a macro the compiled code was only one line.

{% highlight text %}
console.log("2 + 2 = %d", (2 + 2));
{% endhighlight %}

This is only an incidental benefit of using macros. We still need to look at the real benefits. Rather than learn when to use macros, it is better to learn when _not_ to use macros. Macros can be dangerous. Consider this function:

{% highlight text %}
(var square
  (function (x)
    (* x x)))

(console.log (square 2))
{% endhighlight %}

The above code will print the answer `4`.

This can be rewritten as a macro:

{% highlight text %}
(macro square (x)
  (* ~x ~x))

(console.log (square 2))
{% endhighlight %}

And the expanded code is:

{% highlight text %}
(console.log (* 2 2))
{% endhighlight %}

That's it! The answer is correct. But now try the following:

{% highlight text %}
(var i 2)
(console.log (square i++))
{% endhighlight %}

Ouch! You get 6! An embarrassing square of an integer. If you had used the function you would have got the correct answer. This is what happened:

{% highlight text %}
var i = 2;
console.log((i++ * i++));
{% endhighlight %}

When you use functions the arguments to the function get evaluated and then passed into the function. So in this case when you pass `i++`, the value 2 is passed as `x` into the function and `i` gets incremented. So `(x * x)` yields 4. In the case of the macro the argument is not evaluated when the macro expansion happens. Whatever you pass as arguments to the macro just get substituted as is in the template. So if you pass `i++`, it gets substituted as is in your macro template yielding `(i++ * i++)` which is `(2 * 3)`!

###Conclusion

By taking advantage of tree structures and homoiconicity, LispyScript offers an alternative way of developing JavaScript programs.  Although macros are powerful, they must be handled with care.
