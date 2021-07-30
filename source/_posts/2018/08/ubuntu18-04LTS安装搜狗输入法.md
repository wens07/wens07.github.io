---
title: ubuntu18.04LTS安装搜狗输入法
date: 2018-08-24 16:52:02
updated: 2018-08-24 16:52:02
categories: technique
tags: tool
keywords: [ubuntu, sougou, 搜狗]
toc:
---

### 卸载ibus

`sudo apt remove ibus`


### 清除ibus配置

`sudo apt purge ibus`

<!-- more -->

### 卸载顶部面板任务栏上的键盘指示

`sudo  apt remove indicator-keyboard`

### 安装fcitx输入法框架 & 切换为 fcitx输入法

`sudo apt install fcitx-table-wbpy fcitx-config-gtk && im-config -n fcitx`

### 重启让im-config配置生效

`sudo shutdown -r now`

### 下载安装sougou输入法

`wget http://cdn2.ime.sogou.com/dl/index/1524572264/sogoupinyin_2.2.0.0108_amd64.deb?st=ryCwKkvb-0zXvtBlhw5q4Q&e=1529739124&fn=sogoupinyin_2.2.0.0108_amd64.deb`
`sudo dpkg -i sogoupinyin_2.2.0.0108_amd64.deb`

若有错误，修复损坏的包
`sudo apt-get install -f`

### 打开fcitx输入法配置

进行配置sougou输入法