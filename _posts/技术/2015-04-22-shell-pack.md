---
layout: post
title: "打包Shell脚本"
description: ""
category: 技术
tags: [Shell]
---

有时候给别人分享一个工具的时候，同时需要提供的文件比较多；

如果分享一个压缩包还得教会对方如何解压、执行哪个脚本，感觉需要传输的内容多了就不方便；

把几个Shell脚本和文件打包成一个“单独的可执行文件”
 
对方接收到这个文件，只需要执行一下这个文件，就可以实现解压、执行对应脚本了，相对比较方便；

脚本链接：

[Shell_Pack](https://gist.github.com/scue/ac1cc4da7f7fee538e13)

使用方法：

    # single_package: 打包生成文件
    # shell.sh: 解包时运行的脚本文件
    # file1,2,n: 期望一起打包进来的文件
    ./shell_pack.sh -p <single_package> -s <shell.sh> file1 file2 file3 .. 

使用举例:

    ./shell_pack.sh -p logcat_install -s logcat_install.sh logcat_all.sh logcat_wrapper.sh vmstat2

将产生可执行文件`logcat_install`，执行`logcat_install`时，会解压自身文件内的tar.gz文件，并执行关键的脚本`logcat_install.sh`
