---
layout: post
title: "OpenGrok建立Android源码索引"
description: ""
category: 技术
tags: [Android, OpenGrok]
---

### 部署过程

前提条件，使用Ubuntu 12.04及以上64位系统，确保正常连接互联网

    sudo -i
    apt-get install -y openjdk-7-jdk tomcat7 ctags
    wget https://java.net/projects/opengrok/downloads/download/opengrok-0.12.1.5.tar.gz
    tar zxvf opengrok-0.12.1.5.tar.gz -C /usr/local/share/
    /usr/local/share/opengrok-0.12.1.5/bin/OpenGrok deploy

之后浏览器打开`http://localhost:8080/source`，检查Tomcat和OpenGrok是否已正常工作

### 配置SVN

**使用Git管理的请忽略这一段**

首先，要使用SVN克隆一下源代码，假定输出在`/path/to/your_source` 

    svn co /path/to/svn_repo /path/to/your_source --username your_name --password your_password

保存SVN用户、密码

    svn list --username your_name --password your_password # 先让Root存储一次你的svn用户密码，后边会使用到

不生成SVN历史（Android系统项目，源代码量太大了）

    export OPENGROK_GENERATE_HISTORY=off # 每次index前需执行

### 生成索引

    /usr/local/share/opengrok-0.12.1.5/bin/OpenGrok index /path/to/your_source # 数据将保存在 /var/opengrok/

### 每日更新

假定你期望每天凌晨零点自动更新，执行 `sudo crontab -e`，增加以下行

    0 0 * * * /usr/local/share/opengrok-0.12.1.5/bin/OpenGrok index /path/to/your_source

理论上说，使用`OpenGrok updateQuietly`应该也是可以，暂时还没有尝试这样子去更新～

### 权限控制

鉴于一些公司对网络安全的管控，搭建好的源码索引不期望把对所有工程师开放

搭建好之后，我一直没有找到好一点的权限控制，所以就使用了 iptables 来控制哪些IP可以访问

1.  先禁止所有IP可以访问

        sudo iptables -A INPUT -p tcp -m tcp --dport 8080 -j DROP
        sudo iptables -A INPUT -p udp -m udp --dport 8080 -j DROP

2.  然后把能够访问的IP，插入filter这表里

    插入表之前，先使用 -C 参数执行检查

        # tcp
        sudo iptables -C INPUT -s $ipaddress -p tcp --dport 8080 -j ACCEPT || \
            sudo iptables -I INPUT -s $ipaddress -p tcp --dport 8080 -j ACCEPT
        # udp
        sudo iptables -C INPUT -s $ipaddress -p udp --dport 8080 -j ACCEPT || \
            sudo iptables -I INPUT -s $ipaddress -p udp --dport 8080 -j ACCEPT

也可以使用这个脚本进行批量添加: [OpenGrok权限控制脚本](https://gist.github.com/scue/6f6d02738f4e4e3474c3)
