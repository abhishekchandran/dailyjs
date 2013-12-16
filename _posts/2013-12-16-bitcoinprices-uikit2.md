---
layout: post
title: "UIkit 2.0, bitcoinprices.js"
author: Alex Young
categories:
- ui
- libraries
- bitcoin
---

###UIKit

![UIKit 2.0](/images/posts/uikit2.png)

[UIKit 2.0](http://www.getuikit.com/) (GitHub: [uikit / uikit](https://github.com/uikit/uikit), License: _MIT_) is a frontend framework that provides components for layout, navigation, and more complex UI widgets like dropdown replacements.  It uses jQuery and FontAwesome.  Version 2 has just been released, which has some new features including a Markdown editor that supports syntax highlighting and an extensible toolbar.

There's [extensive documentation](http://www.getuikit.com/docs/components.html) and [a theme tool](http://www.getuikit.com/docs/customizer.html), so you can have a look at the main features quite easily.

###bitcoinprices.js

[bitcoinprices.js](http://miohtama.github.io/bitcoin-prices/index.html) (GitHub: [miohtama / bitcoin-prices](https://github.com/miohtama/bitcoin-prices), License: _MIT_) by Mikko Ohtamaa is a client-side library for fetching Bitcoin prices.  It supports currency selection, and uses [BitcoinAverage](https://bitcoinaverage.com/) as the price API.

[BitcoinAverage itself](https://github.com/bitcoinaverage/bitcoinaverage) is an open source Python project that monitors multiple exchanges for prices:

>  Price is a weighted average. Meaning that for every exchange the last trade price and last 24h trading volume is taken, each exchange contributes to the final price only to the extent of it's current trading volume. For a more detailed arithmetics explanation check here.

It's got a nice and simple Bootstrap-based website with graphs and tables.
