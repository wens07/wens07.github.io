---
title: ubuntu LTS安装软件
date: 2018-08-24 16:52:02
updated: 2024-2-25 10:52:02
categories: technique
tags: tool
keywords: [ubuntu, tool, install]
toc:
---

## 安转sogou输入法
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

## 安装、更新gcc版本以及各个版本选择
1. install gcc
```bash
sudo apt update
sudo apt install build-essential
gcc --version
```

2. update apt list & add gcc test repo
```bash
sudo apt update
sudo apt install software-properties-common
sudo add-apt-repository ppa:ubuntu-toolchain-r/test
```

3. install the needed gcc version
```bash
sudo apt update
sudo apt install gcc-13 g++-13 -y
```
4. handle and set serveral gcc versions
```bash
sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-13 13 --slave /usr/bin/g++ g++ /usr/bin/g++-13
sudo update-alternatives --config gcc
```
