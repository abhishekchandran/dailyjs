---
layout: post
title: "Signature Pad, Windows 8.1 Apps with Open Source JavaScript"
author: Alex Young
categories:
- ui
- windows
- mobile
- canvas
---

###Signature Pad

[Signature Pad](http://szimek.github.io/signature_pad/) (GitHub: [szimek / signature_pad](https://github.com/szimek/signature_pad), License: _MIT_) by Szymon Nowak is a client-side library for drawing smooth signatures.  It works with touchscreens and desktop browsers, and was inspired by the [Smoother Signatures](http://corner.squareup.com/2012/07/smoother-signatures.html) post on Square's (excellent) engineering blog.

> The problem is that the signer's finger did not move in straight lines from point to point when tracing out this shape. Rather, our touch points are sampled from a full curve that the signer's finger traced on the touchscreen. While we can't know the original shape between the sampled points Android gave us, straight lines are not the best guess.

Szymon's implementation doesn't depend on any external libraries, and can draw signatures from DATA URIs.

{% highlight javascript %}
var canvas = document.querySelector('canvas');
var signaturePad = new SignaturePad(canvas); 
signaturePad.clear();     // Clears the canvas
signaturePad.toDataURL(); // Returns signature image as data URL
signaturePad.fromDataURL('data:image/png;base64,iVBORw0K...') // Draws signature image from data URL
{% endhighlight %}

###Building a Windows 8.1 App using Typescript and Open Source Libraries

<div class="image">
  <img src="/images/posts/windows8storeexample.png" alt="" />
  <small>Ingredimeals!</small>
</div>

[This screencast by Ala Shiban](http://www.alashiban.com/building-a-windows-8-1-app-using-typescript-and-opensource/) demonstrates how to use some of Microsoft's technologies with open source projects like AngularJS to create a Windows Store application.

> I put together a 17 minute video that gets you started with writing a native Win8.1 app using HTML, CSS, JavaScript, TypeScript, AngularJS, Bootstrap, underscore, BankersBox and jQuery. The goal of the tutorial is to go through the end-to-end experience of developing a win8.1 app as quickly as possible while not developing a random 'hello world' app.

It's a fast screencast that packs a lot in, so if you can't keep up check out the source at [AlaShiban / Ingredimeals](https://github.com/AlaShiban/Ingredimeals).  It uses [TypeScript](http://www.typescriptlang.org/), Blend for Visual Studio, NuGet, jQuery, AngularJS, Underscore, and Bootstrap.  Custom fonts are used to give the application a Windows 8 feel.

I haven't used Windows 8 or Visual Studio much before, so I thought it was interesting seeing how it integrated with third-party open source JavaScript libraries through NuGet, and how debugging JavaScript worked.

Something I hadn't seen before was [MSApp.execUnsafeLocalFunction](http://msdn.microsoft.com/en-us/library/windows/apps/hh767331.aspx).  I noticed Ala had to wrap some calls inside AngularJS (mainly things that wrote to `innerHTML`) to satisfy Microsoft's security requirements for Windows Store apps.
