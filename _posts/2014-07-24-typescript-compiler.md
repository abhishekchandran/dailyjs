---
layout: post
title: "TypeScript's Compiler"
author: "Alex Young"
categories:
- typescript
- languages
- microsoft
---

<div class="intro">
  <p>This week on DailyJS every post is about TypeScript!  This article is all about TypeScript's compiler.</p>
</div>

This week a new [TypeScript compiler was announced](http://blogs.msdn.com/b/typescript/archive/2014/07/21/new-compiler-and-moving-to-github.aspx), along with the move of the project to GitHub.

> Our work to date on the new compiler has been very promising.  At its current level of completeness, the new compiler is able to compile existing real-world TypeScript code 5x faster than the currently shipping compiler.  These results are still early. Once the compiler has reached parity, we'll be able to report out a more complete picture of the performance improvements.

You might be wondering how the TypeScript compiler works.  The source can be found at [GitHub: Microsoft/TypeScript](https://github.com/Microsoft/TypeScript/tree/master/src/compiler), and is written in TypeScript.  It's structured using features and idioms commonly used in TypeScript, like services and generics.

There's a parser, scanner, and the infrastructure needed to work with command-line options and files.  The parser generates nodes that are used by an "emitter" that produces the desired output.  You'll see a lot of switch statements matching on enums that relate to language constructs.

### Comparison with Other Compilers

The CoffeeScript parser is generated from a [Jison](http://github.com/zaach/jison) file -- so unlike TypeScript it has an additional context free grammar file.  There are [attempts at writing Jison-based TypeScript compilers](https://github.com/benjaminjackman/jison-typescript-compiler), which are interesting to look at.  [LiveScript](http://livescript.net/) is also based on Jison.

[ClojureScript's compiler](https://github.com/clojure/clojurescript/blob/master/src/clj/cljs/compiler.clj) transforms ClojureScript into JavaScript.  Originally ClojureScript was written in Clojure, and I'm not sure if it's self-hosted yet.  [There was a fork that is self-hosted](https://github.com/lazerwalker/clojurescript-in-clojurescript), however.

### Automation

One issue with JavaScript compilers is the fact you have to recompile files to JavaScript whenever you make a change.  Fortunately, `tsc` has a `--watch` option, so you can write `tsc -w file.ts` to watch for changes on `file.ts`.  This can easily be used with a module like [nodemon](https://github.com/remy/nodemon) to automatically restart the Node process (if you're using Node) as well.

There are also Grunt and Gulp plugins for TypeScript:

* [gulp-typescript](https://www.npmjs.org/package/gulp-typescript)
* [grunt-typescript](https://www.npmjs.org/package/grunt-typescript)


### Conclusion

It's interesting that there seems to be three main approaches to transpiling JavaScript:

* Parser based on a context-free grammar
* Self-hosted hand-written parser
* External language

If someone had showed me TypeScript I would have assumed it was written with a CLR-based language, so it's cool that it's self-hosted and able to easily run without Microsoft's development tools.
