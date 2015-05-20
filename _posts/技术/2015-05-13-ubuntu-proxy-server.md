---
layout: post
title: "Ubuntu代理服务器配置"
description: ""
category: 技术
tags: [Ubuntu,Proxy]
---

### Squid3

这个合适做`http_proxy`代理服务器

1.  安装方法

        sudo apt-get install squid

2.  修改配置`sudo vi /etc/squid3/squid.conf`，找到并修改

        http_access allow all #注释掉其他的Deny

    然后注释后其他的Deny即可

3.  启动方法

        sudo service squid3 restart

4.  其他很有用的配置`sudo vi /etc/squid3/squid.conf`

        # Server存在多IP，不同网段访问
        acl ip_1 myip 123.123.88.70/22
        acl ip_2 myip 123.123.139.70/22

        acl t200_0 dst 123.123.88.0/22      
        acl t200_1 dst 123.123.0.0/22      
        acl t200_2 dst 123.123.72.0/22      
        acl t200_3 dst 123.123.136.0/22      
        acl t200_4 dst 123.123.164.0/22      
        acl t200_5 dst 123.123.192.0/22      

        tcp_outgoing_address t200_0 ip_1
        tcp_outgoing_address t200_1 ip_2
        tcp_outgoing_address t200_2 ip_2
        tcp_outgoing_address t200_3 ip_2
        tcp_outgoing_address t200_4 ip_2
        tcp_outgoing_address t200_5 ip_2

        # Server监听端口
        http_port 12345

        # 隐藏Client真实IP
        forwarded_for delete

### Socks5

这个相对容易，直接使用一行命令即可

    autossh -CgNfD 0.0.0.0:1080 vps-ssl

-   `-C`:            启用压缩
-   `-g`:            允许远程连接到本地转发的端口
-   `-N`:            登录后不要执行命令行
-   `-f`:            使命令行后台运行
-   `-D`:            绑定Socks Proxy到本地端口
-   `0.0.0.0:1080`:  表示所有IP都可以访问到1080这个端口

### `Socks5 Proxy` to `Http Proxy`

使用软件`privoxy`，安装方法

    sudo apt-get install privoxy

修改配置`sudo vi /etc/privoxy/config`，修改或增加以下配置

    listen-address  0.0.0.0:1081
    forward-socks5   /               127.0.0.1:1080 .
