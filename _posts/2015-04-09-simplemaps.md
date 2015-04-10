---
layout: post
title: "Introduction to SimpleMaps"
author: Chris Youderian
image: "/images/posts/simplemaps-1.png"
categories:
- tutorial
- maps
- geoip
- data
- libraries
- sponsored-content
---

<div class="sponsored-content">
  <p><a class="label" href="/sponsored-content.html">Sponsored Content</a> This post is about a commercial product that we think will appeal to DailyJS readers.</p>
</div>

Interactive maps are a great way to visualize geographic data or improve website navigation.  Now that SVG is supported by all modern browsers, it has become a popular format for interactive maps.  Vector maps scale beautifully and are an attractive and lightweight alternative to Google Maps and OpenStreetMap.

[SimpleMaps](http://simplemaps.com) is a commercial interactive map library.  It adds region-level zooming, responsiveness, legacy browser support, latitude/longitude calibration, mobile-friendly tooltips and more to an otherwise static SVG file.  If you'd prefer to implement these features on your own, it also offers a free library of web-optimized [SVG maps](http://simplemaps.com/resources/svg-maps) (MIT licensed).

This tutorial will demonstrate what is possible with SimpleMaps and how to get started. To begin, go to [http://simplemaps.com/world](http://simplemaps.com/world) and download the world map trial.  Open `test.html` in a web browser to view the map.

![Initial](/images/posts/simplemaps-1.png)

The map consists of two JavaScript files:  `worldmap.js` and `mapdata.js`.  The vector paths and the map logic are stored in the `worldmap.js` file.  All customizations to the map are stored in the `mapdata.js` file.  The map can be easily customized by making changes to the `mapdata.js` file in a text editor and refreshing the browser.  

The `mapdata.js` file contains defaults that can be overwritten for individual countries.  For example, to make all countries red, you would simply set:

{% highlight javascript %}
state_color: 'red',
{% endhighlight %}

in the `main_settings` object.  To override that default and make the USA blue, you'd simply add:

{% highlight javascript %}
color: 'blue',
{% endhighlight %}

to the US `state_specific` object. The `description` property for each country accepts HTML which will be displayed in the tooltip upon hover or (when a mobile device is detected) click.

To speed up the customization process, SimpleMaps offers an online customization tool that makes it easy to customize properties quickly using a spreadsheet.  Countries, locations, and regions can all be customized using this Excel-like interface.  Changes to the map are reflected in real time.

![Customization](/images/posts/simplemaps-2.png)

All customizations are automatically saved to the `mapdata.js` file.  This makes it easy to switch between the convenience of the spreadsheet editor and the control of making changes directly to the JavaScript object.  It is even possible to edit the JavaScript code online using the "Code" tab.

![Code](/images/posts/simplemaps-3.png)

When you are finished, you can install the map on a webpage by embedding both scripts and adding a target `<div>`:

{% highlight html %}
<script type="text/javascript" src="mapdata.js"></script>
<script type="text/javascript" src="worldmap.js"></script> 
<div id="map"></div>
{% endhighlight %}

To fully integrate SimpleMaps with other web page elements you can utilize its [JavaScript API](http://simplemaps.com/docs/api).  This makes it possible to update the map, listen for map events, and dynamically zoom around the map.

All around, SimpleMaps aims to simplify the process of creating interactive maps while retaining the flexibility that has made SVG maps so popular.
