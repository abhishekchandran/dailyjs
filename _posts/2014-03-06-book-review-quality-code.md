---
layout: post
title: "Book Review: Quality Code: Software Testing Principles, Practices, and Patterns"
author: Alex Young
categories:
- books
- testing
- jquery
---

![Quality Code](/images/posts/qualitycode.png)

[Quality Code: Software Testing Principles, Practices, and Patterns](http://www.informit.com/store/quality-code-software-testing-principles-practices-9780321832986) ($44.99, eBook:  $35.99, Addison-Wesley Professional) by Stephen Vance is a book about testing.  It uses examples from several languages -- Java is the most prominent, but there are JavaScript examples as well.  The most significant part for DailyJS readers is a long practical exercise that involves testing an open source jQuery plugin, but there is a lot of general software design advice that you will find useful.

The book introduces automated testing, but also discusses how tests can be managed in real teams.  One of the main points here is how the same best practices that you use for production code should go into automated tests -- if you use certain object oriented patterns, small methods, SOLID principles, and so on, then these techniques should be used for test code as well.

This leads into the practice of writing maintainable test code: the relationship between engineering and craftsmanship.

> Civil engineers may supervise and inspect the building of bridges or buildings, but they spend little time driving rivets, pouring concrete, or stringing suspension cables. Probably the closest to software engineers' total immersion might be the handful of test pilots who are also aeronautical engineers, in that they participate in design, construction, inspection, and verification of the craft they fly.

There are JavaScript examples for code coverage issues, dynamic dispatch, scope, asynchronous computation and promises, and Jasmine:

> Dynamic languages like JavaScript are less tied to an explicit interface, although usage still defines a de-facto interface. Jasmine's `spyOn` functionality provides the full range of test-double variations by substituting a test-instrumented recording object for the function being replaced and letting you define how it behaves when invoked.

What I learned most from, though, was the higher-level advice, like "test the error paths":

> Many people stop before testing the error handling of their software. Unfortunately, much of the perception of software quality is forged not by whether the software fails, because it eventually will, but by how it handles those failures.

And the following point reinforced the way I work, mixing "spec"-like tests with integration and unit tests:

> I prefer to test each defect, at least at the unit level.

Stephen sometimes talks about how most of our programming languages and tools aren't designed specifically to support testing.  One idea that runs through the book is about how to design code to be testable, and writing decoupled tests is part of this.  Balancing encapsulation with access to internal state for testing is something that I think most of us struggle with.

> As we have seen, verification of those internal representations sometimes occurs through interface access. Where null safety is either guaranteed by the representation or ignored by the test, we see code like `A.getB().getC().getD()`
> Despite the blatant violation of the Principle of Least Knowledge, we frequently find code like this-of course we do not write it ourselves!— in tests and production.

Chapter 12, "Use Existing Seams", left an impression on me: it's about the idea of finding places in code that allows you to take control of that code so you can bring it under test.  Since reading that chapter I seem to have found more convenient places to grapple Express applications and test them more thoroughly.

If you write tests, but find they become unmaintainable over time, then this book may guide you to create less entangled tests.  It mixes material for dynamic languages like JavaScript with statically typed languages such as C++ and Java.  I find this useful as someone who writes a lot of JavaScript but works alongside Objective-C and .NET developers.

Stephen has combined years of experience into a rare, testing-focused book, that relates principles that we use to write well-designed code to the problems inherent in automated testing.
