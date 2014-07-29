---
layout: post
title: "BitcoinJS 1.0"
author: "Alex Young"
categories:
- bitcoin
- libraries
---

[BitcoinJS 1.0](http://bitcoinjs.org/) (GitHub: [bitcoinjs / bitcoinjs-lib](https://github.com/bitcoinjs/bitcoinjs-lib), License: _MIT_, npm: [bitcoinjs-lib](https://www.npmjs.org/package/bitcoinjs-lib)) has been released.  This is a library for working with Bitcoins.  For example, `Bitcoin.ECKey.makeRandom` can be used to generate a new address, and you can create transactions with `new Bitcoin.Transaction()`.

The API is clean and easy to learn, and it comes with a test suite.  It depends on [crypto-js](https://www.npmjs.org/package/crypto-js) and some modules for working with base 58 encoding.  Typed arrays are used to ensure it has solid performance.

BitcoinJS is a popular module, and is used by some popular Bitcoin-related services, including Hive Wallet, Blockchain.info, and BitAddress.

It comes with support for browsers, so you can use it in client-side code as well as Node.

The 1.0 release signifies a milestone that the author has been working on since 2011.  For more details, see the [1.0 announcement](http://bitcoinjs.org/announce-1.0.0.txt).
