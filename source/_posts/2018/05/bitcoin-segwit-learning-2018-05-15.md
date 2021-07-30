---
layout: "post"
title: bitcoin-segwit-learning
date: 2018-05-15 10:29:13
updated:
categories: [cryptocurrency]
tags: [blockchain]
keywords: [blockchain, bitcoin]
toc:
---

## segwit相关
### segwit bips
see [bitcoin bip141](https://github.com/bitcoin/bips/blob/master/bip-0141.mediawiki)
    [bitcoin bip143](https://github.com/bitcoin/bips/blob/master/bip-0143.mediawiki)
    [bitcoin bip144](https://github.com/bitcoin/bips/blob/master/bip-0144.mediawiki)
    [bitcoin bip147](https://github.com/bitcoin/bips/blob/master/bip-0147.mediawiki)
    (chain activated on August 24, 2017)


### block cost calculation
    cost = (stripped_size * 4) + witness_size formula,
    using only serialization with and without witness data. As witness_size
    is equal to total_size - stripped_size, this formula is identical to:
    cost = (stripped_size * 3) + total_size.







