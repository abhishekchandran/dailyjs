---
layout: post
title: "Introduction to ChocolateChip-UI"
author: "Robert Biggs"
categories: 
- browser
- tutorials
- ui
---

<div class="intro">
This post is a tutorial about <a href="http://www.chocolatechip-ui.com/">ChoculateChip-UI</a> from Sourcebits Inc.
</div>

We're going to look at how to throw together a simple navigable app with the [ChocolateChip-UI](http://www.chocolatechip-ui.com/) framework. This will require familiarity with HTML. You don't need to be good with CSS or even know how to write JavaScript. ChocolateChip-UI provides functionality out of the box to provide functionality for Web apps. 

ChocolateChip-UI uses a particular combination of simple tags to define the structures that make up a mobile app. These are: **nav**, **article**, **section**, **ul**, **li**, **div**, **aside**, **span**, **p** and **h1** through **h5**.

To follow along, [download the framework](https://github.com/sourcebitsllc/chocolatechip-ui/archive/master.zip) and grab the folder "chui". This contains the files that comprise ChocolateChip-UI. We're going to use three files: chocolatechip-3.0.4.min.js, chui-3.0.4.min.js and chui-ios-3.0.4.min.js.

To make a Web page behave like an app in the browser, we need to first provide some meta tags. Here is the basic skeleton with appropriate meta tags and links to the ChocolateChip-UI resources:

{% highlight html %}
<!doctype html>
<html lang="en">
<head>
  <meta name="viewport" content="initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
  <meta name="apple-mobile-web-app-capable" content="yes">
  <meta name="msapplication-tap-highlight" content="no">
  <meta charset="UTF-8">
  <title>Document</title>
  <link rel="stylesheet" href="chui/chui.ios-3.0.4.min.css">
  <script src="chui/chocolatechip-3.0.4.min.js"></script>
  <script src="chui/chui-3.0.4.min.js"></script>
</head>
<body>
</body>
</html>
{% endhighlight %}

The app will reside inside of the body tag. When you look at the screen of a mobile devices, you notice that most apps use two main parts to present everything on the screen: a nav bar and everything below that. ChocolateChip-UI uses a combination of a `nav` tag and an `article` tag to create each screen of the app. Since we're going to make a navigable app, we'll need to put together a number of screen, each consisting of a `nav` and `article`.

The first screen will be the current view, and all others with be upcoming. ChocolateChip-UI designates this navigation status using two classes: "current" and "next".

Every `nav` will have at least an `h1`, which is the title that appears in the navigation bar. Let's start building this. We'll need to create a navigation bar and an article. ChocolateChip-UI forces the article to fill the screen. Every article should have one child -- a `section` tag. All the content will go in the `section`. It will automatically provide inertia scrolling when the user swipes.

Every `article` tag must have a unique id. This is used during navigation so that ChocolateChip-UI knows where to go and where to return to. If you find at some time that your app is not going to where you want or not returning properly, check that your articles have the ids they need and that you have all uses of them spelled identically.

Here is the basic app shell.

{% highlight html %}
<!doctype html>
<html lang="en">
<head>
  <meta name="viewport" content="initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
  <meta name="apple-mobile-web-app-capable" content="yes">
  <meta name="msapplication-tap-highlight" content="no">
  <meta charset="UTF-8">
  <title>Document</title>
  <link rel="stylesheet" href="chui/chui.ios-3.0.4.min.css">
  <script src="chui/chocolatechip-3.0.4.min.js"></script>
  <script src="chui/chui-3.0.4.min.js"></script>
</head>
<body>
  <nav class="current">
    <h1>Fruits</h1>
  </nav>
  <article class="current" id="fruits">
    <section></section>
  </article>
</body>
</html>
{% endhighlight %}

You'll notice that when it loads in the browser, the title appears in a nav bar, but there is nothing below that. ChocolateChip-UI uses unordered lists with the class `list` to display tabular data. We can give the list a title by putting an `h2` right before the list. To display data in each list item, we use an `h3` as the title and an `h4` as the subtitle and a paragraph tag as the item detail. If we put the class `nav` on a list item, we get the right facing caret that iOS uses to indicate a navigable item.

[Source code, part 3](https://gist.github.com/alexyoung/b669a17486adda476d09#file-part3-html)

To make this list able to navigate to other articles, we need to indicate where each list item should go. We do this using an HTML5 data attribute: `data-goto`. We give it the id of the article to which it will go. This will result in automatic navigation when the article that it points to exists.

This example includes the `data-` attributes:

[Source code, part 4](https://gist.github.com/alexyoung/b669a17486adda476d09#file-part4-html)


Here's what the navigation list should look like so far:

![Navigation list](/images/posts/chui-1.png)

Now we need to add an article with the id for each fruit: apples, oranges, bananas, mangos and avocados. We'll also want to provide a `nav` with an `h1` with the title of each fruit. Because these navs and articles are not current in navigation, we need to explicitly give them the class `next`. This will put them out of view until the navigation occurs.

[Source code, part 5](https://gist.github.com/alexyoung/b669a17486adda476d09#file-part5-html)

This creates a navigable app, except for one problem. After the user selects a fruit and the app navigates to that screen, there is no way to get back. We can provide a way back by adding a back button in each nav bar right before the title.

[Source code, part 6](https://gist.github.com/alexyoung/b669a17486adda476d09#file-part6-html)

![Detail page of Navigation list](/images/posts/chui-2.png)

To complete our simple app we just need to add a list to each of the fruit articles. We can use the same pattern we used on the main article.

[Source code, part 7](https://gist.github.com/alexyoung/b669a17486adda476d09#file-part7-html)

To support Android or Windows Phone 8, you just need to switch out the reference in the CSS link: chui/chui.ios-3.0.4.min.css. Change `ios` for `android` or `win`.

Of course, this is just the most basic setup for an app. In real life you would want to get data dynamically through Ajax requests and output it to your app using templates. Sounds like another article.

