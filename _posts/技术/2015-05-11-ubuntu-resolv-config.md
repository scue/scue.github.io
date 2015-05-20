---
layout: post
title: "ubuntu域名解析配置"
description: ""
category: 技术
tags: [Ubuntu]
---

有些时候我们会发现莫名其妙的不能上网，包括 `apt-get update` 或网络浏览器访问解析 都有可能出现问题

一般这种情况，有可能是我们域名解析服务器没有配置，或者是 `sudo` 执行的时候没找到域名解析服务器

设定方法：

编辑文件 `sudo vi /etc/resolvconf/resolv.conf.d/head`，添加内容

    nameserver 180.76.76.76
    nameserver 114.114.114.114

然后再执行 `sudo resolvconf -u` 更新到系统就好了，Enjoy!
