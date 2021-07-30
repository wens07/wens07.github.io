---
layout: "post"
title: "shadowsocks安装"
date: "2017-11-10 13:50"
categories: technique
tags: [tool]
keywords: [shadowsocks, proxy]
toc:
---

## shadowsocks-libev 版本安装

### centos 7(64) 系统
- 前提准备

    安装一些必要的软件以及依赖
    ```
    yum install git vim wget -y
    yum install epel-release -y
    yum install gcc gettext autoconf libtool automake make pcre-devel asciidoc xmlto udns-devel libev-devel mbedtls-devel -y
    ```
<!-- more -->

- 下载shadowsocks-libev源码

  ```
  git clone https://github.com/shadowsocks/shadowsocks-libev.git
  cd shadowsocks-libev
  git submodule update --init --recursive
  ```

- 开始进行编译

  1. 安装依赖libsodium 和 MbedTLS

  ```
  export LIBSODIUM_VER=1.0.13
  wget https://download.libsodium.org/libsodium/releases/libsodium-$LIBSODIUM_VER.tar.gz
  tar xvf libsodium-$LIBSODIUM_VER.tar.gz
  pushd libsodium-$LIBSODIUM_VER
  ./configure --prefix=/usr && make
  make install
  popd
  ldconfig

  export MBEDTLS_VER=2.6.0
  wget https://tls.mbed.org/download/mbedtls-$MBEDTLS_VER-gpl.tgz
  tar xvf mbedtls-$MBEDTLS_VER-gpl.tgz
  pushd mbedtls-$MBEDTLS_VER
  make SHARED=1 CFLAGS=-fPIC
  sudo make DESTDIR=/usr install
  popd
  sudo ldconfig
  ```

  2. 编译shadowsocks-libev

  ```
  ./autogen.sh && ./configure --prefix=/usr && make
  make install
  ```

- 修改配置文件

  ```
  mkdir -p /etc/shadowsocks-libev
  vim /etc/shadowsocks-libev/config.json
  ```

  config.json 内容如下
  ```
  {
	"server":["[::0]","0.0.0.0"],
	"server_port":自定端口号,
	"local_port":1080,
	"password":"自定密码",
	"timeout":60,
	"method":"aes-256-gcm"
  }
  ```


- 设置开机启动

  `vi /etc/systemd/system/shadowsocks.service`

  shadowsocks.service 内容如下
  ```
  [Unit]
  Description=Shadowsocks Server
  After=network.target
  [Service]
  ExecStart=/usr/bin/ss-server -c /etc/shadowsocks-libev/config.json -u
  Restart=on-abort
  [Install]
  WantedBy=multi-user.target
  ```

  `systemctl enable shadowsocks`


- shadowsocks服务的启动 & 停止 & 更新

  1. 如果centos开启了防火墙(firewalld), 我们还不能通过外网访问服务器，因为防火墙并没有开启相应的端口

    添加相应的端口
    `vi /etc/firewalld/zones/public.xml`

    添加如下行:
    ```
    <port protocol="tcp" port="服务器端口"/>
    <port protocol="udp" port="服务器端口"/>
    ```

    使规则生效
    `firewall-cmd --complete-reload`

  2. 启动
    `systemctl start shadowsocks`

  3. 停止
    `systemctl stop shadowsocks`

  4. 重启
    `systemctl restart shadowsocks`

  5. 查看状态
    `systemctl status shadowsocks`





  6. 更新
    - 先停止ss服务
      `systemctl stop shadowsocks`

    - 切换到shadowsocks-libev目录
      ```
      git pull
      ./configure
      make
      make install

      systemctl start shadowsocks
      ```
