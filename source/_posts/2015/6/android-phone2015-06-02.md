---
title: android phone
date: 2015-06-02 00:58:23
categories: technique
tags: android
keywords: [android, adb]
toc:
---

### 更改/添加or删除系统文件

1. usb连接手机到电脑上
`adb devices`

2. 取得root权限
`adb root`

3. 重新挂载
`adb remount`

4. 进行添加or删除
`adb pull/push xxxx`

<!-- more -->

### 在手机内部上操作

1. 进入到手机内部
`adb shell`

2. 使用pm/am管理安装包和程序的活动
`pm install/uninstall`
`am`
