---
layout: "post"
title: "markdown-file-commands"
date: "2016-10-07 13:28"
categories: technique
tags: [markdown]
keywords: markdown
toc:
---
### 上标和下标
- 上标： `O(n<sup>2</sup>)`

   效果 O(n<sup>2</sup>)

- 下标: `O(h<sub>2</sub>o)`

   效果 O(h<sub>2</sub>o)


### 插入图片
- 语法: `![the name to show](the path of the image)`
  ![boost source architecture](/images/2016/boost source architecture.png)
<!-- more -->

### 插入链接
- 语法: `[linker name](the site address)`

### 插入文章链接
- 语法: `{% post_link post_name_in_posts_dir %}`

### 加粗/斜体
- 加粗: **the content**
- 斜体: *the content*


### mathjax

- $content$, 语句中的公式
- $$content$$  单独居中表示的公司
- {}  公式中的group
- ^, _  上标以及下标 

### 换行

某行后面额外加两个空格