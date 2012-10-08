---
layout: post
title: "Decorating Your JavaScript"
author: "Justin Naifeh"
categories:
- pattern
- object-oriented
- decorator
---

The [decorator pattern](https://en.wikipedia.org/wiki/Decorator_pattern), also known as a wrapper, is a mechanism by which to extend the run-time behavior of an object, a process known as decorating. The pattern is often overlooked because its simplicity belies its object-oriented benefits when writing scalable code. Decorating objects is also neglected in JavaScript because the dynamic nature of the language allows developers to abuse the malleability of objects, but **just because you can doesn't mean you should**.

Before delving into the decorator pattern, let's examine a realistic coding problem that can be solved with other solutions. The decorator is best understood after the shortcomings of other common solutions have been explored.

###The Problem

You are writing a simple archiving tool that manages the display and lifecycle of publications and their authors. An important feature is the ability to list the contributing authors, which may be a subset of all authors. The default is to show the first three authors of any publication. The initial domain model is basic:

![domain](/images/posts/decorator-domain.png)

Using plain JavaScript we implement the read-only classes as follows:

{% highlight javascript %}
/**
 * Author constructor.
 *
 * @param String firstName
 * @param String lastName
 */
var Author = function(firstName, lastName) {
  this._firstName = firstName;
  this._lastName = lastName;
};

Author.prototype = {

  /**
   * @return String The author's first name.
   */
  getFirstName: function() {
    return this._firstName;
  },

  /**
   * @return String The author's last name.
   */
  getLastName: function() {
    return this._lastName;
  },

  /**
   * @return String The representation of the Author.
   */
  toString: function() {
    return this.getFirstName()+' '+this.getLastName();
  }
};

/**
 * Publication constructor.
 *
 * @param String title
 * @param Author[] authors
 * @param int type
 */
var Publication = function(title, authors, type) {
  this._title = title;
  this._authors = authors;
  this._type = type;
};

Publication.prototype = {

  /**
   * @return String The publication title.
   */
  getTitle: function() {
    return this._title;
  },

  /**
   * @return Author[] All authors.
   */
  getAuthors: function() {
    return this._authors;
  },

  /**
   * @return int The publication type.
   */
  getType: function() {
    return this._type;
  },

  /**
   * A publication might have several authors, but we
   * are only interested in the first three for a standard publication.
   *
   * @return Author[] The significant contributors.
   */
  contributingAuthors: function() {
    return this._authors.slice(0, 3);
  },

  /**
   * @return String the representation of the Publication.
   */
  toString: function() {
    return '['+this.getType()+'] "'+this.getTitle()+'" by '+this.contributingAuthors().join(', ');
  }
};
{% endhighlight %}

The API is straightforward. Consider the following invocations:

{% highlight javascript %}
var pub = new Publication('The Shining', 
  [new Author('Stephen', 'King')],
  'horror');

// rely on the default toString() to print: [horror] "The Shining" by Stephen King
alert(pub);

// ...

var pub2 = new Publication('Design Patterns: Elements of Reusable Object-Oriented Software', [
  new Author('Erich', 'Gamma'),
  new Author('Richard', 'Helm'),
  new Author('Ralph', 'Johnson'),
  new Author('John', 'Vlissides')
], 'programming');

// prints: [programming] "Design Patterns: Elements of Reusable Object-Oriented Software" by Erich Gamma, Richard Helm, Ralph Johnson
alert(pub2);
{% endhighlight %}

The design is simple and reliable...at least until the client specifies a new requirement:

> In accordance with the convention for [medical publications](https://www.ncbi.nlm.nih.gov/pubmed/17651671), only list the first (primary) and last (supervisor) authors if multiple authors exist.

This means that if `Publication.getType()` returns "medical" we must perform special logic to list the contributing authors. All other types (e.g., horror, romance, computer, etc) will use the default behavior.

###Solutions

There are many solutions to satisfy the new requirement, but some have disadvantages that are not readily apparent. Let's explore a few of these and see why they are not ideal even though they are commonplace.

####Overwrite Behavior
{% highlight javascript %}
// overwrite the contributingAuthors definition
if (pub.getType() === 'medical') {
  pub.contributingAuthors = function() {
    var authors = this.getAuthors();

    // return the first and last authors if possible
    if (authors.length > 1) {
      return authors.slice(0, 1).concat(authors.slice(-1));
    } else {
      return authors.slice(0, 1);
    }
  }
}
{% endhighlight %}

This, one could argue, can be the most abused feature of the language: the ability to arbitrarily overwrite properties and behavior at run-time. Now the `if/else` condition must be maintained and expanded if more requirements are added to specify contributing authors. Furthermore, it is debatable whether or not `pub` is still an instance of `Publication`. A quick [instanceof](https://developer.mozilla.org/en-US/docs/JavaScript/Reference/Operators/instanceof) check will confirm that it is, but a class defines a set of state and behavior. In this case we have modified select instances and the calling code can no longer trust the consistency of `Publication` objects.

####Change the Calling Code

{% highlight javascript %}
var listing;
if (pub.getType() === 'medical') {
  var contribs = pub.getAuthors();

  // return the first and last authors if possible
  if (contribs.length > 1) {
    contribs = contribs.slice(0, 1).concat(contribs.slice(-1));
  } else {
    contribs = contribs.slice(0, 1);
  }

  listing = '['+pub.getType()+'] "'+pub.getTitle()+'" by '+contribs.join(', ');
} else {
  listing = pub.toString();
}

alert(listing);
{% endhighlight %}

This solution violates encapsulation by forcing calling code to understand the internal implementation of `Publication.toString()` and recreate it outside of the class. A good design should not burden calling code.

####Subclass the Component

![subclass](/images/posts/decorator-subclass.png)

One of the most common solutions is to create a `MedicalPublication` class that extends `Publication`, with a `contributingAuthors()` override to provide custom behavior. While this approach is arguably less flawed than the first two, it pushes the limit of clean inheritance. We should always [favor composition](https://en.wikipedia.org/wiki/Composition_over_inheritance) over inheritance to avoid overreliance on the [base class internals](https://en.wikipedia.org/wiki/Fragile_base_class) (for the [developer masochists](http://www.cas.mcmaster.ca/~emil/Publications_files/MikhajlovSekerinski98FragileBaseClassProblem.pdf)).

Subclassing also fails as a viable strategy when more than one customization might occur or when there is an unknown combination of customizations. An often cited example is a program to model a coffee shop where customers can customize their cup of coffee, thus affecting the price. A developer could create subclasses that reflect the myriad combinations such as `CoffeeWithCream` and `CoffeeWithoutCreamExtraSugar` that override `Coffee.getPrice()`, but it is easy to see that the design will not scale.

####Modify the Source Code

{% highlight javascript %}
contributingAuthors: function() {
  if (this.getType() === 'medical') {
    var authors = this.getAuthors();

    if (authors.length > 1) {
      return authors.slice(0, 1).concat(authors.slice(-1));
    } else {
      return authors.slice(0, 1);
    }
  } else {
    return this._authors.slice(0, 3);
  }
}
{% endhighlight %}

This is somewhat of a hack, but in a small project where you control the source code it might suffice. A clear disadvantage is that the `if/else` condition must grow with every custom behavior, making it a potential maintenance nightmare.

Another thing to note is that you should never, ever modify source code outside of your control. Even the mention of such an idea should leave a taste in your mouth worse than drinking orange juice after brushing your teeth. Doing so will inextricably couple your code to that revision of the API. The cases where this is a valid option are so few and far between that it is usually an architectural issue in the application, not in the outside code.

###The Decorator

These solutions fulfill the requirement at the cost of jeopardizing maintainability and scalability. As a developer you must pick what is right for your application, but there is one more option to examine before making a decision.

I recommend using a decorator, a flexible pattern by which to extend the behavior of your existing objects. The following UML represents an abstract implementation of the pattern:

![decorator uml](/images/posts/decorator-uml.png)

The `ConcreteComponent` and `Decorator` classes implement the same `Component` interface (or extend `Component` if it's a superclass). The `Decorator` keeps a reference to a `Component` for delegation except in the case where we "decorate" by customizing the behavior.

By adhering to the `Component` contract, we are guaranteeing a consistent API and guarding against implementation internals because calling code **will not** and **should not** know if the object is a `ConcreteComponent` or `Decorator`. Programming to the interface is the cornerstone of good object-oriented design.

> Some argue that JavaScript is not object-oriented, and while it supports prototypical inheritance instead of classical, objects are still innate to the language. The language supports [polymorphism](https://en.wikipedia.org/wiki/Polymorphism_in_object-oriented_programming) and that fact that all objects extend `Object` is sufficient to argue the language is object-oriented as well as functional.

###The Implementation

Our solution will use a slight variant of the decorator pattern because JavaScript does not have some classical inheritance concepts such as interfaces or abstract classes. There are many libraries that simulate such constructs, which is beneficial for certain applications, but here we will use the languages basics.

![publication](/images/posts/decorator-publication.png)

The class `MedicalPublication` and `Publication` implicitly implement `PublicationIF`. In this case `MedicalPublication` acts as the decorator to list the first and last authors as contributors while unchanging other behavior.

Note that `MedicalPublication` references `PublicationIF`, and not `Publication`. By referencing the interface instead of a specific implementation we can arbitrarily nest decorators within one another! (In the coffee shop problem we can create decorators such as `WithCream`, `WithoutCream`, and `ExtraSugar`--these can be nested to handle any complex order.)

The `MedicalPublication` class delegates for all standard operations and overrides `contributingAuthors()` to provide the "decorated" behavior.

{% highlight javascript %}
/**
 * MedicalPublication constructor.
 *
 * @param PublicationIF The publication to decorate.
 */
var MedicalPublication = function(publication) {
  this._publication = publication;
};

MedicalPublication.prototype = {

  /**
   * @return String The publication title.
   */
  getTitle:  function() {
    return this._publication.getTitle();
  },

  /**
   * @return Author[] All authors.
   */
  getAuthors: function() {
    return this._publication.getAuthors();
  },

  /**
   * @return int The publication type.
   */
  getType: function() {
    return this._publication.getType();
  },

  /**
   * Returns the first and last authors if multiple authors exists.
   * Otherwise, the first author is returned. This is a convention in the
   * medical publication domain.
   *
   * @return Author[] The significant contributors.
   */
  contributingAuthors: function() {

    var authors = this.getAuthors();

    if (authors.length > 1) {
      // fetch the first and last contributors
      return authors.slice(0, 1).concat(authors.slice(-1));
    } else {
      // zero or one contributors
      return authors.slice(0, 1);
    }
  },

  /**
   * @return String the representation of the Publication.
   */
  toString: function() {
    return 'Decorated - ['+this.getType()+'] "'+this.getTitle()+'" by '+this.contributingAuthors().join(', ');
  }
};

/**
 * Factory method to instantiate the appropriate PublicationIF implementation.
 *
 * @param String The discriminating type on which to select an implementation.
 * @param String The publication title.
 * @param Author[] The publication's authors.
 * @return PublicationIF The created object.
 */
var publicationFactory = function(title, authors, type) {

  if (type === 'medical') {
    return new MedicalPublication(new Publication(title, authors, type));
  } else {
    return new Publication(type, title, authors);
  }
};
{% endhighlight %}

By using the factory method we can safely create an instance of PublicationIF.

{% highlight javascript %}
var title = 'Pancreatic Extracts as a Treatment for Diabetes';
var authors = [new Author('Adam', 'Thompson'), 
  new Author('Robert', 'Grace'), 
  new Author('Sarah', 'Townsend')];
var type = 'medical';

var pub = publicationFactory(title, authors, type);

// prints: Decorated - [medical] 'Pancreatic Extracts as a Treatment of Diabetes' by Adam Thompson, Sarah Townsend
alert(pub);
{% endhighlight %}

In these examples we are using `toString()` for brevity and debugging, but now we can create utility classes and methods to print `PublicationIF` objects for application display.

![printer](/images/posts/decorator-printer.png)

Once the application is modified to expect `PublicationIF` objects we can accommodate further requirements to handle what constitutes a [contributing author](https://en.wikipedia.org/wiki/Academic_authorship) by adding new decorators. Also, the design is now open for any `PublicationIF` implementations beyond decorators to fulfill other requirements, which greatly increases the flexibility of the code.

###Criticisms

One criticism is that the decorator must be maintained to adhere to its interface. All code, regardless of design, must be maintained to a degree, but it can be argued that maintaining a design with a clearly stated contract and pre- and post-conditions is much simpler than searching `if/else` conditions for run-time state and behavior modifications. More importantly, the decorator pattern safeguards calling code written by other developers (or even yourself) by leveraging object-oriented [principles](https://en.wikipedia.org/wiki/Open/closed_principle).

Another criticism is that decorators must implement all operations defined by a contract to enforce a consistent API. While this can be tedious at times, there are [libraries](http://jsclass.jcoglan.com/decorator.html) and methodologies that can be used with JavaScript's dynamic nature to expedite coding. Reflection-like invocation can be used to allay concerns when dealing with a changing API.

{% highlight javascript %}
/**
 * Invoke the target method and rely on its pre- and post-conditions.
 */
Decorator.prototype.someOperation = function() {
  return this._decorated.someOperation.apply(this._decorated, arguments);
};

// ... or a helper library can automatically wrap the function

/**
 * Dynamic invocation.
 *
 * @param Class The class defining the function.
 * @param String The func to execute.
 * @param Object The *this* execution context.
 */
function wrapper(klass, func, context) {
  return function() {
    return klass.prototype[func].apply(context, arguments);
  };
};
{% endhighlight %}

The details are up to the developer, but even the most primitive decorator pattern is extremely powerful. The overhead and maintenance for the pattern itself is minimal, especially when compared to that of the opposing solutions.

###Conclusion

The decorator pattern is not flashy, despite its name, nor does it give the developer bragging rights in the "Look at what I did!" department. What the decorator does do, however, is correctly encapsulate and modularize your code to make it scalable for future changes. When a new requirement states that a certain publication type must list all authors as contributors, regardless of ordinal rank, you won't fret about having to refactor hundreds of lines of code. Instead, you'll write a new decorator, drop it into the factory method, and take an extra long lunch because you've earned it.
