---
layout: "post"
title: "blockchain -- encryption and decryption"
date: "2017-05-18 16:49"
categories: cryptocurrency
tags: [blockchain]
keywords: [blockchain, encryption, decryption]
toc:
---

### 数字签名算法(digital signature algorithm)
*ECDSA (elliptic curve digital signature algorithm)*
secp256k1(the parameters of ecdsa used in bitcoin)

1. private key: 32 bytes(256 bit)
2. compressed or uncompressed public key: 33 bytes / 65 bytes
3. signature or compact_signature: 72 bytes/ 65 bytes
<!-- more -->

### derive key algorithm
1. scrypt
2. pbkdf2

### proof of stake 
1. the node(producing block) selection:
    two most commonly used methods: 'Randomised Block Selection' and  'Coin Age Selection'

### dpow 

**also see post in {% post_link bitcoin-2017-05-19 %}**