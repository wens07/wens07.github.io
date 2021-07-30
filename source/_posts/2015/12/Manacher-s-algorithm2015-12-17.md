---
layout: post
title: "Manacher's algorithm"
date: 2015-12-17 11:17:32
categories: technique
tags: algorithm
keywords: "Manacher's algorithm"
toc:
---

> if  p[i'] <= R - i; then p[i] = p[i']
  else p[i] >= R -i (which we should expand i (the center) past the rigth edge to get it)
