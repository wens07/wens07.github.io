---
layout: post
title: mac osx 破解wpa/wpa2 wifi
date: 2016-01-06 23:35:26
categories: technique
tags: [mac, tool]
keywords: [wifi, hack, crack]
toc:
---

在mac osx下进行wpa/wpa2 加密的wifi破解

- 首先要安装`aircrack-ng`工具
```
#可以使用Homebrew进行安装

brew install aircrack-ng
```
如果安装过程中出现下载失败, [这篇文章](/2016/01/06/brew-手工下载文件安装/)

- 用airport搜索附近wifi
```
sudo airport -s
```
<!-- more -->
结果如下图所示:
![airport -s output](/images/2016/airport_s.png)
- 根据搜索出的wifi进行嗅探
```
sudo airport ***en0*** sniff ***1***
```
上面的en0为wifi card所在的地址, 有的也可能为en1, 可以根据实际情况输入, 可从以下地方获得:
![wifi card addr](/images/2016/wificard_addr.png)

1为你所要嗅探的wifi所在的CHANNEL.

默认嗅探的所存的文件在/tmp中, 以airportSniff****.cap形式命名.

- 最后就是使用aircrack-ng和下载的密码字典进行暴力破解
```
aircrack-ng -w wordlist airportSniff****.cap
```
一般输入如下所示:
![aircrack-ng run output](/images/2016/aircrack-ng.png)

看上面cap文件内的抓包内容, Encryption列中找到WPA (1 handshake)---它表示抓包成功. 当然要找到你想破解wifi的成功抓包, 然后在「Index number of target network?」中输入该成功抓包所在的行号. 此示例中为1:
![index number](/images/2016/index number.png)

破解过程如下:
![aircrack-ng running](/images/2016/running.png)

如果破解成功, 会显示 KEY FOUND!:
![aircrack-ng crack successfully](/images/2016/aircrack-ng success.jpg)
