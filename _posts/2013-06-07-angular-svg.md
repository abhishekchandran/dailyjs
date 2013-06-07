---
layout: post
title: "AngularJS and SVG"
author: John Munsch
categories:
- angularjs
- svg
- tutorials
- guest-post
---

<div class="intro">
  <p>John Munsch is a professional software developer with over 26 years of experience. These days he's building modern web app front ends with AngularJS after a couple of years spent doing the same kind of work with Backbone.js, Underscore.js, and Handlebars.js.</p>
  <p>For some reason odd reason everybody thinks he's a front end guy these days despite most of his career being spent in the Java, C++, and C world.</p>
  <p>This article was originally published at <a href="http://johnmunsch.wordpress.com/2013/06/03/changeable-vector-graphics-with-svg-and-angularjs/">johnmunsch.wordpress.com/</a>.</p>
</div>

I've long been a fan of using SVG (Scalable Vector Graphics) to do images that I can change easily on the fly. When I say "long been a fan" I mean that when I first started doing it I hand wrote some SVG as XML to show a donation bar we needed for GameDev.net and I had a program that would change the amount thus far donated on the bar and run it through an early version of the Java Batik library to spit out a JPEG file we could put on the website. It was crude, but it sure beat making a new graphic two or three times a day.

Years later things have gotten a lot easier. Modern browsers have advanced to the point where you can include an SVG image in the page as easily as referring to them in an img tag like so, &lt;img src="something.svg"/&gt;, or just dumping some SVG code straight into the middle of the HTML for your page like this &lt;svg&gt;...lots of vector graphics...&lt;/svg&gt;. And editing? Why would you edit by hand anymore when Adobe Illustrator can generate SVG files of your drawings for you, or if you have no budget for such nice tools, <a href="http://inkscape.org/">Inkscape</a> does a pretty good job and costs nothing.

So it occurred to me the other day that it would be interesting to see if I could use AngularJS and its ability to rewrite HTML on the fly and combine that with SVG in the browser to rewrite SVG on the fly. The answer is, it not only works, it's downright easy to do so. I've provided a couple of different examples to show just how easy it is to so.

###Example 1: SVG with AngularJS Model Values

Getting an image to start with was pretty easy. I went to <a href="http://thenounproject.com/">The Noun Project</a> and grabbed an icon of the sun I liked. It was provided by an unknown author in this case. The icon came in SVG format so all I did with it in Inkscape was add a little color and some text that showed the temperature. Then I saved that as a "Plain SVG" file rather than an "Inkscape SVG" file. It might have worked as well with the latter but I didn't want any surprises.

<div class="image">
  <img src="/images/posts/inkscape-editing-svg-icon.png" alt="" />
  <small>Editing an SVG icon.</small>
</div>

I then popped over to an HTML file I had generated and imported it with an image link like this:

{% highlight html %}
<img alt="" src="images/sunshine_plus_temp.svg" />
{% endhighlight %}

I then hand edited the SVG file and found where the text for the temperature and replaced it with an AngularJS model variable reference. So:

{% highlight html %}
<tspan sodipodi:role="line" id="tspan4542" x="97.124313" y="52.063747">87°</tspan>
{% endhighlight %}

became:

{% highlight html %}
<tspan sodipodi:role="line" id="tspan4542" x="97.124313" y="52.063747">{{temp}}°</tspan>
{% endhighlight %}

The &lt;img&gt; way of loading the SVG had to change because AngularJS wasn't going to replace a variable inside an image for me. So I simply pasted the contents of the sunshine_plus_temp.svg right into the middle of a page already setup for AngularJS and put the temp variable into my $scope. It worked like a charm. With an input field tied to the model variable, as I typed, the SVG graphic was automatically updated with the new value.

My final touch was to externalize the SVG file. Nobody wants to edit an HTML file with half a dozen or more embedded lumps of SVG in there. It could quickly turn into an unreadable mess. And, as I already observed, &lt;img&gt; won't work either. Ah, but AngularJS jumps to the fore again because it has it's ng-include directive. All I had to do was this:

{% highlight html %}
<span ng-include="'images/sunshine_plus_temp.svg'"></span>
{% endhighlight %}

and AngularJS was including the image where I needed it and binding the variable to the model for real-time update. Here's the final version of the code I came up with for my first example, note the second set of quotes inside the ng-include to tell it not to interpret the string inside there, it's just a string to use directly:

{% highlight html %}
  <div>
    <p>Example 1: Text updated on the fly in an SVG graphic via AngularJS.</p>
    <span ng-include="'images/sunshine_plus_temp.svg'"></span>
  </div>
  <label>Temperature</label> <input type="text" ng-model="temp"/>
{% endhighlight %}

It's worth noting that Inkscape is still perfectly capable of editing the SVG file even after the change I made and I guess I could have just made the change within Inkscape in the first place and never bothered opening up the file to manually change it with a text editor.

<div class="image">
  <img src="/images/posts/inkscape-editing-modified-svg-icon.png" alt="" />
  <small>Editing an SVG icon that has been modified by AngularJS.</small>
</div>

###Example 2: Incorporating an Image

We don't really need a second example here, the first one showed pretty much everything but I wanted to show how easily images incorporate into SVG and help you achieve results that would be much much harder to do with other techniques. In this example I took a slides icon by Diego Naive, from The Noun Project, overlaid an image on top of it, and then overlaid a glossy reflection on top of half the slide, just to show that the image is fully incorporated by the graphic and can easily be rotated, have graphics on top of it, underneath it, etc. Stuff that would require a lot of work to do with many other techniques.

Again, I tested it out and edited the final SVG file to add a variable reference, in this case to {{slide_image}} instead of the specific file reference that I had added with Inkscape. This time, I will say that it does not edit nearly as well in Inkscape after the edit because it doesn't know where to find an image named "{{slide_image}}". Within the Inkscape editor you just see an error box where the image should be. Not perfect, but not debilitating either.

Here's a page with links to both examples and to the GitHub repository with all the code for both: <a href="http://johnmunsch.github.io/AngularJSExamples/">http://johnmunsch.github.io/AngularJSExamples/</a>

