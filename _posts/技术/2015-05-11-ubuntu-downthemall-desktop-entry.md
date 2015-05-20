---
layout: post
title: "Ubuntu DownThemAll快速启动"
description: ""
category: 技术
tags: [Ubuntu]
---

个人比较喜欢Google Chrome，但Chrome默认的下载器容易下载出现问题；

而使用Firefox的插件DownThemAll就不出现这个问题了，但又不期望打开Firefox而直接使用DownThemAll；

可以这么做，编译文件 `~/.local/share/applications/downthemall.desktop`

    [Desktop Entry]
    Type=Application
    Encoding=UTF-8
    Name=DownThemAll
    Comment=
    Exec=firefox -no-remote -chrome chrome://dta/content/dta/addurl.xul
    Icon=firefox
    Terminal=false

保存之后，按下`Alt+F1`，输入`DownThemAll`就可以看到刚刚写好的桌面启动图标了，拖动到启动栏即可
