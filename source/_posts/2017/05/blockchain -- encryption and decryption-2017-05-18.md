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

### DSA && ECDSA
both based on no generally efficient solution to solve a discrete logarithm problem
- DSA: discrete logarithm problem with modular exponentiation
- ecdsa: discrete logarithm problem wiht elliptic curves

### ECDSA && EdDSA
1. using different family of elliptic curve
2. EdDSA While offering slight advantages in speed over ECDSA, its popularity comes from an improvement in security. Instead of relying on a random number for the nonce value, EdDSA generates a nonce deterministically as a hash making it collision resistant