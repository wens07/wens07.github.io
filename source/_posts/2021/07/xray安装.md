---
title: xray安装
date: 2021-07-30 10:15:00
updated: 2021-07-30 10:15:00
categories: technique
tags: [tool]
keywords: [xray, v2ray, proxy]
toc:
---

### centos 7(64) 系统

1. 防火墙

- 查看防火墙是否开启
`firewall-cmd --state`

- 重载防火墙,使新规则生效
`firewall-cmd --complete-reload`

- 查看打开的端口
`firewall-cmd --list-ports`

- 启动&停止 防火墙
`sytemctl start firewalld`
`systemctl stop firewalld`
<!-- more -->
- 开机启动或停止 防火墙
`systemctl enable firewalld`
`systemctl disable firewalld`

2. 添加端口

- 直接编辑规则文件

`vi /etc/firewalld/zones/public.xml`

添加相应端口如下行:
```
<port protocol="tcp" port="服务器端口"/>
<port protocol="udp" port="服务器端口"/>
```

- 命令

`firewall-cmd --zone=public --add-port=port/tcp --permanent`


3. 安装xray & 更新(更新的话在执行一遍即可)

[xray github](https://github.com/XTLS/Xray-install)
