---
layout: post
title: hyperledger
date: 2019-03-028 22:39:40
categories: 
  - [technique]
  - [随笔]
tags: [读书笔记, blockchain]
keywords: ["blockchain", "读书笔记"]
toc:
---

## hyperledger fabric
1. ordering service: broadcast and establish concensus
2. identity and membership
3. scalable dissemination(optional): An optional peer-to-peer gossip service disseminates the blocks output by ordering service to all peers
4. smart-contract execution
5. ledger maintenance

### limitation of Order-Execute architecture
1. sequential execution
2. no deterministic code
3. confidentiality of execution

### fabric Execute-Order-Validation architecture
1. node type
- client: submit transaction proposals  and broadcast them
- peer: execute transaction proposals and validate them and maintain blockchain ledger which is append-only
  not all peers will execute the transaciton proposals, which called endorsing peers execute them.
- ordering service node
