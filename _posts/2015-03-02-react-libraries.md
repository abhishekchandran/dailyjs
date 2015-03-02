---
layout: post
title: "React in Atom, JSX Control Statements, Baobab"
author: Alex Young
image: "/images/posts/jsx-highlight.png"
categories:
- react
- ui
- atom
- ide
---

I seem to have a huge backlog of React-related submissions to the DailyJS inbox, so you might see more React libraries than usual over the next few weeks.  There's no conspiracy to promote React, it's just that readers seem interested in it!

###React in Atom

![React in Atom](/images/posts/jsx-highlight.png)

Jaakko Lukkari sent in [atom-react](http://orktes.github.io/atom-react/) (GitHub: [orktes/atom-react](https://github.com/orktes/atom-react), License: _MIT_), a plugin for the Atom IDE that adds features for React.  The main features are syntax highlighting, indentation, code folding, snippets, JSX reformatting, HTML to JSX conversion, and autocomplete.

The documentation has videos of each of the main features.  This plugin was based on [sublime-react](https://github.com/reactjs/sublime-react), which is a pretty popular Sublime package.

###JSX Control Statements

Asaf Katz sent in JSX Control Statements (GitHub: [valtech-au/jsx-control-statements](https://github.com/valtech-au/jsx-control-statements), License: _MIT_, npm: [jsx-control-statements](https://www.npmjs.com/package/jsx-control-statements)) by Alex Gilleran.  This adds control statements like `If Else` and `For each`:

{% highlight text %}
<If condition={this.props.condition === 'blah'}>
  <span>IfBlock</span>
<Else />
  <span>ElseBlock</span>
</If>
{% endhighlight %}

Loops look like this:

{% highlight text %}
<For each="blah" of={this.props.blahs}>
  <span key={blah}>{blah + this.somethingElse}</span>
</For>
{% endhighlight %}

[JSX doesn't have If-Else](http://facebook.github.io/react/tips/if-else-in-JSX.html), and due to how React works the author has decided to implement these features using JSTransform.  This guards against early evaluation during parsing.  The readme has a more detailed explanation and examples for Webpack and Node-JSX.


###Baobab

Asaf Katz also sent Baobab.  Baobab (GitHub: [Yomguithereal/baobab](https://github.com/Yomguithereal/baobab), License: _MIT_) by Guillaume Plique is a JavaScript data tree supporting cursors.  It's inspired by [Clojure zippers](http://clojuredocs.org/clojure.zip/zipper), and can be used with React through mixins.

Cursors allow you to listen for changes nested within trees, so if your UI is data-driven then you can react to changes to specific parts of objects.

Asaf said that Christian Alfoni's blog post on Baobab really sells the library: [Plant a Baobab tree in your flux application](http://christianalfoni.github.io/javascript/2015/02/06/plant-a-baobab-tree-in-your-flux-application.html):

> A Baobab tree is strictly the state of your application. All of it. Everything exists in one tree. What makes this tree so special is that any changes will trigger an event, but not as you might expect.

Christian uses Baobab with a flux architecture by creating a state tree with Baobab and then rendering the UI with React.  The article explains all of the main terminology, so if you're not used to thinking about Flux, React, immutability and state, then you should get a lot out of this article.
