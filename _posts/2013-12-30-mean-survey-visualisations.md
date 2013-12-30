---
layout: post
title: "Mean, Survey Visualisations"
author: "Alex Young"
categories: 
- express
- node
- mean
- survey
---

###Mean

You want to build a web application, and you need a database.  You can write JavaScript, but you're not yet completely comfortable with Node.  What do you do?

I wrote about [Getting MEAN](http://www.manning.com/sholmes/) recently, a book about building web applications with MongoDB and Express.  If you're interested in this approach, a quick way to get started is [Mean](http://mean.io/) (GitHub: [linnovate / mean](https://github.com/linnovate/mean), License: _MIT_), a module that collects everything you need together.  It even includes AngularJS and Bootstrap, so you get a solid interface out of the box.

If you already understand the MVC pattern, and use AngularJS, then this is definitely a quick way to get started.  It's also a handy way of getting experiments up and running quickly, which is a great way to learn.

###Survey Visualisations

![Survey Visualisations](/images/posts/surveyvis.png)

Konrad Dzwinel sent in these [visualisations of the DailyJS survey](http://kdzwinel.github.io/dailyjs-survey-sankey-diagrams/).  It allows you to see how answers to one question map to another.  This is cool because I wanted to compare "What type of JavaScript do you write?" to "Where do you use JavaScript?" -- I was expecting to see a lot of people writing side projects for the server at home, but the split is pretty even.

The visualisations are powered by [D3.js](http://d3js.org/), and Bootstrap has been used as well.
