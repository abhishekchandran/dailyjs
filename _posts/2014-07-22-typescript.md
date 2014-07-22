---
layout: post
title: "TypeScript Week"
author: "Alex Young"
categories:
- typescript
- languages
- microsoft
---

<div class="intro">
  <p>This week on DailyJS every post is about TypeScript!  The first post introduces the language, and the growing TypeScript community.</p>
</div>

TypeScript might not be as popular as CoffeeScript, but it seems to be catching on with a highly productive niche of developers that are building interesting open source projects.  TypeScript is very much of the new school of Microsoft developers: it embraces Node, open standards, open source, while building on interesting influences from Microsoft Research and .NET.

If you're excited by technologies like C# 5.0's asynchronous support and ReactiveUI, then TypeScript will help you to be more productive with JavaScript.  There's even Visual Studio support!  If you're from a JavaScript client-side or server-side background, however, then it might be harder to appreciate why TypeScript is interesting.

The first thing to consider is that TypeScript adopts ideas from ECMAScript 6, while compiling down to ES3.  This includes features like classes, modules, and a succinct lambda syntax:

{% highlight javascript %}
var deck = {
  suits: ["hearts", "spades", "clubs", "diamonds"],
  cards: Array(52),
  createCardPicker: function() {
    return () => {
      var pickedCard = Math.floor(Math.random() * 52);
      var pickedSuit = Math.floor(pickedCard / 13);
      return { suit: this.suits[pickedSuit], card: pickedCard % 13 };
    }
  }
}
{% endhighlight %}

In this example, the lambda is introduced with `() =>`.  This should be familiar to C# developers, but for the rest of us it feels quite new.  There's a subtle difference to using `function() {}`, however -- lambdas capture `this` in a more intuitive way than standard JavaScript.  In this example, `this.suits` is possible because the lambda binds to the containing object rather than `window`.

TypeScript allows you to write classes with the `class` keyword and inherit with the `extends` keyword.  There's more, though: generics are supported.  Again, the syntax looks like C#, using angle brackets to denote the generic type parameter:

{% highlight javascript %}
class GenericNumber<T> {
  zeroValue: T;
  add: (x: T, y: T) => T;
}

var myGenericNumber = new GenericNumber<number>();
myGenericNumber.zeroValue = 0;
myGenericNumber.add = function(x, y) { return x + y; };
{% endhighlight %}

C# is statically typed, which means... I'm not really qualified to go into a discussion about type systems, so here's a quote from MSDN:

> C# is a strongly-typed language. Every variable and constant has a type, as does every expression that evaluates to a value. Every method signature specifies a type for each input parameter and for the return value. The .NET Framework class library defines a set of built-in numeric types as well as more complex types that represent a wide variety of logical constructs, such as the file system, network connections, collections and arrays of objects, and dates. A typical C# program uses types from the class library as well as user-defined types that model the concepts that are specific to the program's problem domain.

When working with C#, the IDE is able to infer a huge amount of information about your classes and methods.  It scales up nicely on large projects, which means you can be productive despite the build/run cycle.

In fact, TypeScript was inspired by the need to develop tools for using JavaScript on large projects within Microsoft.  That means to use TypeScript you'll have to get used to thinking about types, but it has benefits for writing code that can be partially verified by a compiler, and adhere to contracts (defined by "interfaces").

To interoperate with JavaScript libraries, TypeScript supports hybrid types.  You can even write your own declaration files that tell the TypeScript compiler how to handle a JavaScript library.

With classes, modules, lambdas, and type hints, you might be wondering how TypeScript will fit in with the future of JavaScript now that we know some of these things are coming to ES6.  Apparently Microsoft have stated that TypeScript will be adapted as JavaScript changes. I don't know what kind of backwards incompatibilities this might cause, so it'll be interesting to see how they handle updates to the language specification.

I've seen a lot of negative press about Windows 8 and Microsoft's mobile efforts, but if you're completely outside of the Microsoft ecosystem then I think you should learn more about TypeScript.  Microsoft have contributed to Node, and the adoption of asynchronous and reactive programming in C# has transformed how people write software for Microsoft's platforms.  The developer tools, languages, and libraries are worth learning about and may help you to write better JavaScript in general.  Don't write them off just because it's fashionable to complain about Modern UI!

If you're still confused about TypeScript, get started [on the Wikipedia page](http://en.wikipedia.org/wiki/TypeScript).  It introduces some history behind the language.  For more about the language, [see the language spec](http://www.typescriptlang.org/Content/TypeScript%20Language%20Specification.pdf).  You can also find tutorials on [typescriptlang.org](http://www.typescriptlang.org/), and I found [the handbook](http://www.typescriptlang.org/Handbook) useful for mentally mapping between JavaScript, C#, and TypeScript.
