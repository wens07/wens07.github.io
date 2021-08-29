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

- [xray github](https://github.com/XTLS/Xray-install)

- 相关安装路径

```
installed: /usr/local/bin/xray
installed: /usr/local/share/xray/geoip.dat
installed: /usr/local/share/xray/geosite.dat
installed: /usr/local/etc/xray/config.json
installed: /var/log/xray/
installed: /var/log/xray/access.log
installed: /var/log/xray/error.log
installed: /etc/systemd/system/xray.service
installed: /etc/systemd/system/xray@.servic
```
- 相关文档
XTLS.github.io

- 查看启动日志
`journalctl -xe --no-pager -u xray`

### centos8开启bbr
1. 开启bbr
```
echo "net.core.default_qdisc=fq" >> /etc/sysctl.conf
echo "net.ipv4.tcp_congestion_control=bbr" >> /etc/sysctl.conf
sysctl -p
```

2. 验证是否开启成功
```
sysctl -n net.ipv4.tcp_congestion_control
lsmod | grep bbr
```

### 安装ssl证书
1. 安装acme.sh脚本
`curl  https://get.acme.sh | sh`
安装在: ~/.aceme.sh

2. 使aceme.sh脚本生效
`source .bashrc`

3. 生成证书&安装证书&更新证书
- 生成证书
`acme.sh --issue -d s388419.savps.ru --standalone --keylength ec-256 --force`

- 安装证书
```
mkdir ~/xray_cert
acme.sh --installcert -d s388419.savps.ru --ecc --fullchain-file ~/xray_cert/xray.crt --key-file ~/xray_cert/xray.key

// xray.key add read permission
chmod +r ~/xray_cert/xray.key
```

- 更新证书
> 由于 Let's Encrypt 的证书有效期只有 3 个月，因此需要 90 天至少要更新一次证书，acme.sh 脚本会每 60 天自动更新证书. 也可以手动更新
```
acme.sh --renew -d s388419.savps.ru --force --ecc
acme.sh --installcert -d s388419.savps.ru --ecc --fullchain-file ~/xray_cert/xray.crt --key-file ~/xray_cert/xray.key
```
