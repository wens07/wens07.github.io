---
layout: "post"
title: "markdown-usage"
date: "2016-10-07 13:28"
updated: 2020-03-31 22:39:40
categories:
  - [随笔]
tags: [随笔, markdown]
keywords: ["markdown", "随笔"]
toc:
---
## 上标和下标
- 上标： `O(n<sup>2</sup>)`

   效果 O(n<sup>2</sup>)

- 下标: `O(h<sub>2</sub>o)`

   效果 O(h<sub>2</sub>o)


## 插入图片
- 语法: `![the name to show](the path of the image)`
  ![boost source architecture](/source/images/2016/boost_source_architecture.png)
<!-- more -->

## 插入链接
- 语法: `[linker name](the site address)`

## 插入文章链接
- 语法: `{% post_link post_name_in_posts_dir %}`

## 加粗/斜体
- 加粗: **the content**
- 斜体: *the content*


## mathjax

- `$content$`, 语句中的公式
- `$$content$$`,  单独居中表示的公式
- {}  公式中的group
- ^, _  上标以及下标
- `\frac{分子}{分母}`
- 空格控制: `\quad` or `{\kern ?pt}`

## 换行
- 行尾两个空格或多个空格或换行符
- 使用<br>

## 多级有序列表
下一级做两个空格的缩进

## reference
- '>'
line or multiline reference

- '>>'
nested reference

## 表格
Markdown 表格由 「竖线 |」、「减号 -」、「冒号 :」三种符号组成。

- 竖线 用来定义列，每两个竖线之间为一个单元格元素；
- 减号 用来定义分割线，也就是分割表头和数据体；
- 冒号 配合减号使用，用于定义列数据的对齐属性。