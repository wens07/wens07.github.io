---
layout: post
title: eos
date: 2019-03-06 22:39:40
categories: 
  - [technique]
  - [随笔]
tags: [eos]
keywords: ["eos"]
toc:
---

1. Developer reference site
[EOSIO Developer Portal](https://developers.eos.io/)

2. mainnet & testnet site
[eos mainnet](https://bloks.io/wallet)
[eos jungle2.0 testnet](https://monitor.jungletestnet.io/#home)

<!-- more -->
3. main components
- `cleos`(cli + eos = cleos): command line interface to interact with the blockchain and to manage wallets.
- `nodeos`(node + eos = nodeos): the core EOSIO node daemon that can be configured with plugins to run a node. Example uses are block production, dedicated API endpoints, and local development.
- `keosd`(key + eos = keosd): component that securely stores EOSIO keys in wallets.
- `eosio.cdt`: eos contract devepment toolkit.


4. 获取抵押列表
`cleos -u http://jungle2.cryptolions.io:80  system listbw wenstestnet1`