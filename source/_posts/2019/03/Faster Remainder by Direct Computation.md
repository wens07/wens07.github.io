---
layout: post
title: Faster Remainder by Direct Computation
date: 2019-03-08 20:39:40
categories: 
  - [technique]
  - [随笔]
tags: [algorithm]
keywords: ["fast remainder"]
toc:
---


1. introduction 
  in general, on common processor machine, Integer multiplication is many times faster than division.
So dividing a numerator n by a divisor d is mathematically equivalent to multiplication by the inverse of the divisor 
    `n / d = n * (1/d)`

2. faster remainder algorithm
  for detail, see paper[Faster Remainder by Direct Computation
Applications to Compilers and Software Libraries](https://arxiv.org/pdf/1902.01961.pdf)

  the faster remainder algorithm implemented in c is following(unsigned and signed):
<!-- more -->  
```c
uint32_t d = ...; // your divisor > 0

// c = ceil ( (1 < <64) / d ) ; we take L = N
uint64_t c = UINT64_C (0xFFFFFFFFFFFFFFFF ) / d + 1;

// fastmod computes (n mod d) given precomputed c
uint32_t fastmod ( uint32_t n /* , uint64_t c, uint32_t d */) {
    uint64_t lowbits = c * n;
    return (( __uint128_t ) lowbits * d) >> 64;
}
```

```c
int32_t d = ...; // your non - zero divisor in [ -2147483647 ,2147483647]

uint32_t pd = d < 0 ? -d : d; // absolute value , abs (d)
// c = floor ( (1 < <64) / pd ) + 1; Take L = N + 1
uint64_t c = UINT64_C (0xFFFFFFFFFFFFFFFF ) / pd
+ 1 + (( pd & (pd -1) ) ==0 ? 1 : 0) ;

// fastmod computes (n mod d) given precomputed c
int32_t fastmod ( int32_t n /* , uint64_t c, uint32_t pd */) {
    uint64_t lowbits = c * n;
    int32_t highbits = (( __uint128_t ) lowbits * pd) >> 64;
    // answer is equivalent to (n <0) ? highbits - 1 + d : highbits
    return highbits - (( pd - 1) & (n >> 31) ) ;
}
```


  judge divisiablility
```c
// calculate c for use in lkk_divisible
uint64_t lkk_cvalue ( uint32_t d) {
    return 1 + UINT64_C (0xffffffffffffffff ) / d;
}
// given precomputed c, checks whether n % d == 0
bool lkk_divisible ( uint32_t n, uint64_t c) {
    // rhs is large when c ==0
    return n * c <= c - 1;
}
```


```c
// rotate n by e bits , avoiding undefined behaviors
// cf https :// blog . regehr . org / archives /1063
uint32_t rotr32 ( uint32_t n, uint32_t e) {
    return (n >> e) | ( n << ( ( -e) &31) ) ;
}
// does d divide n?
// d = 2** e * d_odd ; dbar = multiplicative_inverse ( d_odd )
// thresh = 0 xffffffff / d
bool gm_divisible ( uint32_t n,
    uint32_t e, uint32_t dbar ,
    uint32_t thresh ) {
    return rotr32 (n * dbar , e) <= thresh ;
}
// Newton ’s method per Warren ,
// Hacker ’s Delight pp. 246 - -247
uint32_t multiplicative_inverse ( uint32_t d) {
    uint32_t x0 = d + 2 * ((d +1) & 4) ;
    uint32_t x1 = x0 * (2 - d * x0) ;
    uint32_t x2 = x1 * (2 - d * x1) ;
    return x2 * (2 - d * x2) ;
}

```



