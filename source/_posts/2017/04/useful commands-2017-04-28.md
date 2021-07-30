---
layout: "post"
title: "useful commands"
date: "2017-04-28 16:16"
categories: technique
tags: [command]
keywords: command
toc:
---

### linux添加用户的相关命令
1. useradd  添加用户
`useradd -d /home/wengqiang -m wengqiang -s /bin/bash`
创建用户wengqiang

2. usermod 修改创建用户的相关属性
`usermod -s /bin/sh wengqiang`
修改用户wengqiang的登录shell

`usermod -aG sudo wengqiang`
将用户wengqinag加入到sudo group中

3. passwd 修改用户的密码
`passwd wengqiang`


### 修改文件的owner以及group
`chown owner_name:group_name file_name`

<!-- more -->


### linux|mac 产生随机串
1. linux上 `cat /dev/urandom | tr -dc A-Z9 | head -c ${1:-81}`
2. mac上 `cat /dev/urandom | LC_ALL=C tr -dc 'A-Z9' | fold -w 81 | head -n 1`


### windows下验证校验码命令
`Certutil`(Certutil /?)

```
certutil -hashfile xxx MD5
certutil -hashfile xxx SHA1
certutil -hashfile xxx SHA256
```

### 获取本机ip

`curl https://ip.cn`


### 使用openssl生成secp256k1的key-pair

1. 生成
`openssl ecparam -name secp256k1 -genkey -out ec-priv.pem`

2. 输出
`openssl ec -in ec-priv.pem -text -noout`


### linux 磁盘相关命令

1. blkid
列出机器上设备的uuid或label等信息

2. pvdisplay|pvcreate
显示physical volume相关信息或者创建physical volume

3. lvdisplay|lvcreate|vgextend vgdisplay|vgcreate|vgextend


### clang&g++显示类的内存分布

`clang++ -cc1 -emit-llvm -fdump-record-layouts thefile.cpp`
`g++ -fdump-class-hierarchy -c test.cpp`


### go 
1. go-wrk 
http benchmark utility
`go get github.com/adjust/go-wrk`

2. go tool pprof
get profile info of the program


add following line in import part
`import _ net/http/pprof`

`go tool pprof --seconds=5 localhost:8000/debug/pprof/profile`

3. go-torch
`go get github.com/uber/go-torch`




### 检测端口是否使用

1. tcp port
`telnet ip port`

2. udp port
`netcat(nc) -vnzu ip port`


### windows添加启动程序

1. 用户下
`win + r` `shell:startup` 打开当前用户的启动目录，将程序的快捷方式放入其中即可

2. 系统下
"C:\ProgramData\Microsoft\Windows\Start Menu\Programs\StartUp"


### 安装bundle插件

1. install Vundle.vim in .../bundle folder
2. `nvim +PluginInstall +qall`


### linux下查看c++编译后的symbols
`nm a.out | grep c++filt`

### vim 保存时获得sudo权限
`:w !sudo tee %`

### 查看连接的top10的用户ip
`netstat -nat | awk '{print $5}' | awk -F ':' '{print $1}' | sort | uniq -c | sort -rn | head -n 10`

### 查看最常用10个命令
`cat .bash_history | sort | uniq -c |  sort -rn | head -n 10`