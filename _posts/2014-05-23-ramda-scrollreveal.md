---
layout: post
title: "Ramda, AniJS ScrollReveal"
author: "Alex Young"
categories:
- functional
- libraries
- animation
---

###Ramda

![Ramda](/images/posts/ramda.png)

[Ramda](http://buzzdecafe.github.io/code/2014/05/16/introducing-ramda/) (GitHub: [CrossEye / ramda](https://github.com/CrossEye/ramda), License: _MIT_, npm: [ramda](https://www.npmjs.org/package/ramda)) by Scott Sauyet and Buzz de Cafe is a functional library that is similar to Underscore, but has a very different API style.

In Underscore you might filter arrays like this:

{% highlight javascript %}
var validUsersNamedBuzz = function(users) {
  return _.filter(users, function(user) { 
    return user.name === 'Buzz' && _.isEmpty(user.errors); 
  });
};
{% endhighlight %}

But in Ramda you can pass the function first and the array last:

{% highlight javascript %}
var validUsersNamedBuzz = R.filter(R.where({ name: 'Buzz', errors: R.isEmpty }));
{% endhighlight %}

All of Ramda's functions curry automatically, which makes composition easier:

> Because the API is function-first, data-last, you can continue composing and composing until you build up the function you need before dropping in the data. (Hugh Jackson published an [excellent article](http://hughfdjackson.com/javascript/why-curry-helps/) describing the advantages of this style.)

These API decisions mean Ramda feels like native JavaScript with less syntax than you might expect.

###ScrollReveal Using AniJS

[ScrollReveal](http://anijs.github.io/examples/scrollreveal/) (GitHub: [anijs / examples / scrollreveal](https://github.com/anijs/examples/tree/gh-pages/scrollreveal)) by Dariel Noel Vila Plagado is an AniJS helper function that animates components as they enter the viewport.

The syntax for animating items looks like this:

{% highlight html %}
<div id="item" data-anijs="if: scroll, on: window, do: swing animated, before: scrollReveal">
  Cuba 2022
</div>
{% endhighlight %}

