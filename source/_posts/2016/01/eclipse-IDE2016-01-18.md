---
layout: post
title: eclipse IDE
date: 2016-01-18 19:22:23
categories: technique
tags: tool
keywords: [eclipse, tool]
toc:
---

### 配置toolchain
> 一般在mac下选择 `MacOSX GCC`, linux 下选择`Linux GCC`
1. 然后可以配置gcc (可以自己源码编译或者下载编译好的hpc gcc)[hpc gcc](http://hpc.sourceforge.net/)
![hpc-gcc](/images/2016/hpc-gcc.png)

2. 配置eclipse使用该版本gcc
  - 配置preference(应用于全部项目)
![eclipse preference](/images/2016/gcc-preference.png)

  - 配置项目的属性（应用于单个项目）
![eclipse project property](/images/2016/eclipse-project-property.png)


### 删除一整行
1. 使用shutcuts：`command + d`
2. 按鼠标左键3下，然后按delete键

<!-- more -->
