---
layout: post
title: "React Native"
author: Alex Young
image: "/images/posts/react-native.png"
categories:
- react
- ios
- android
---

![React Native]("/images/posts/react-native.png")

The developers at Facebook have been showing off [React Native](http://facebook.github.io/react-native/) for a few months, but it's finally been released on GitHub: [facebook/react-native](https://github.com/facebook/react-native).  I went to a Facebook tech talk about React Native earlier this month, and as someone who has experience developing iOS apps, I was extremely excited about it.

React Native lets you write React components with JSX that are converted to native views.  In the Facebook tech talk, they basically described it as being close to ReactJS but with a few functions changed to output native view code instead of DOM elements.  That means React Native apps include a JavaScript runtime.  It also uses a flexbox layout model and styling.  Styles are not written in CSS but instead use JavaScript objects that will make you think of a JSON version of CSS.  Here's an example:

{% highlight javascript %}
tyles = StyleSheet.create({
  row: { flexDirection: 'row', margin: 40 },
  image: { width: 40, height: 40, marginRight: 10 },
  text: { flex: 1, justifyContent: 'center'},
  title: { fontSize: 11, fontWeight: 'bold' },
  subtitle: { fontSize: 10 },
});
{% endhighlight %}

Working with React Native has several benefits:

* You can write components with JavaScript
* Changing views doesn't require recompilation, you see live updates in the iOS simulator
* No recompilation is necessary after fixing crashes that are limited to the JavaScript portion of the project

The way I understood React Native was that it would replace the view and "view model" layer of an application.  You could theoretically write a lot of JavaScript instead of Objective-C, but it seems better to treat it more like front-end development in a web application.  The React Native documentation states that it's designed to work with custom native views:

> It is certainly possible to create a great app using React Native without writing a single line of native code, but React Native is also designed to be easily extended with custom native views and modules - that means you can reuse anything you've already built, and can import and use your favorite native libraries. To create a simple module in iOS, create a new class that implements the RCTBridgeModule protocol, and add RCT_EXPORT to the function you want to make available in JavaScript.

There's a [getting started guide](http://facebook.github.io/react-native/docs/getting-started.html#content) which should help you if you just want to try it out right now, but you'll need to be familiar with Xcode and iOS development.

An Android version is coming, and but will require that your Android apps include the JavaScript runtime.  The iOS version is slightly slicker in that the JavaScript runtime is available as part of Apple's standard libraries (JavaScriptCore).


