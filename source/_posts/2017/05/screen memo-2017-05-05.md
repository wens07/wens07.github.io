---
layout: "post"
title: "screen memo"
date: "2017-05-05 11:44"
categories: technique
tags: [tool]
keywords: screen
toc:
---

### 创建screen
`screen`
`screen -S  "new screen name"`

note: 创建新的screen窗口

### 连接上detach的screen
`screen -r screen-id/thread-id`

note: 默认用screen不带参数生成的窗口的前面的数字screen id也就是thread id

### 连接上attached的screen
`screen -x screen-id/thread-id`

### detach一个窗口以及kill一个窗口
`ctrl-a + d`: detach a window
`ctrl-a + k`: kill a window

<!-- more -->
