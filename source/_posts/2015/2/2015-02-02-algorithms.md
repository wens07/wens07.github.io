---
title: algorithms
date: 2015-02-02 16:27:18
updated: 2023-11-07
categories: technique
tags: algorithm
keywords: algorithm
---

## Divide and Conquer(Main Thoery)

if a>=1 and b > 1, T(n) = aT(n/b) + f(n)

1. case 1
$$
 f(n) = O(n^{\log_b{a-\epsilon}}) \longrightarrow T(n) = \Theta(n^{\log_ba})
$$

2. case 2
$$
 f(n) = \Theta(n^{\log_ba}) \longrightarrow T(n) = \Theta(n^{\log_ba}\lg n)
$$
<!-- more -->
3. case 3
$$
 f(n) = \Omega(n^{\log_b{a+\epsilon}}) \longrightarrow T(n) = \Theta{f(n)})
$$


## Fibonacci 数列近似值
$$
	f(n) \approx 2^{0.694n} \approx (1.6)^{n}
$$

## 对于排序数组的组合
可以做到$$O(n{\log_2{n}})$$
Given a nonempty subset of indices S, define the children of S to be S \ {max(S)} U {max(S) + 1} and S U {max(S) + 1}
![the subset of S](/source/images/2024/subset_example1.png)
![the subset of S](/source/images/2024/subset_example2.png)