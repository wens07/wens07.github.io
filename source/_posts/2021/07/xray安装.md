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


3. 安装v2ray & 更新(更新的话在执行一遍即可)
`### centos 7(64) 系统

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


3. 安装v2ray & 更新(更新的话在执行一遍即可)
`bash <(curl -L https://raw.githubusercontent.com/v2fly/fhs-install-v2ray/master/install-release.sh)`

4. 创建配置文件（/etc/v2ray/config.json）


5. 验证配置文件 && 生成uuid
`/usr/bin/v2ray/v2ray --test -config=/path/to/config.json`
输出configuration ok即为合法的配置

`/usr/bin/v2ray/v2ctl uuid`

6. v2ray命令
`service v2ray start|stop|status|reload|restart|force-reload `
`systemctl enable/disable v2ray`

7. 修改ssh端口
`vim /etc/ssh/sshd_config` 找到port修改
`/etc/init.d/sshd restart` 重启ssh服务
`

4. 创建配置文件（/etc/v2ray/config.json）


5. 验证配置文件 && 生成uuid
`/usr/bin/v2ray/v2ray --test -config=/path/to/config.json`
输出configuration ok即为合法的配置

`/usr/bin/v2ray/v2ctl uuid`

6. v2ray命令
`service v2ray start|stop|status|reload|restart|force-reload `
`systemctl enable/disable v2ray`

7. 修改ssh端口
`vim /etc/ssh/sshd_config` 找到port修改
`/etc/init.d/sshd restart` 重启ssh服务
