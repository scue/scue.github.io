---
layout: post
title: "Windows安装youcompleteme"
description: ""
category: 技术
tags: [Windows]
---

### 安装vim

直接安装一个`http://rj.baidu.com/soft/detail/12314.html`

**值得注意的是Windows的VIM程序只有32位的**

### 安装Python环境

因为vim只有32位的，所以，安装Python的时候也只能安装Python 32位版本

这里我选择的是Python2.7.9，32位版本，（安装时记得勾选选择设定环境变量到系统）

### 安装youcompleteme

1.  下载youcompleteme

    [vim-ycm-733de48-windows-x86.zip](https://bitbucket.org/Haroogan/vim-youcompleteme-for-windows/downloads/vim-ycm-733de48-windows-x86.zip)

    解压压缩包到你想解压的目录，比如我选择的是，然后我会使用`pathogen`去加载它

        %HOMEPATH%\.vim_runtime\plugins_for_me_win\vim-ycm-733de48-windows-x86

2.  下载llvm

    [llvm-3.4-mingw-w64-4.8.1-x86-posix-sjlj.zip](https://bitbucket.org/Haroogan/llvm-for-windows/downloads/llvm-3.4-mingw-w64-4.8.1-x86-posix-sjlj.zip)

    下载LLVM只需要其中一个文件`libclang.dll`，把它拷贝到`vim-ycm-733de48-windows-x86\third_party\ycmd\libclang.dll`

    在我这里的路径是

        %HOMEPATH%\.vim_runtime\plugins_for_me_win\vim-ycm-733de48-windows-x86\third_party\ycmd\libclang.dll

3.  安装ctags[可选项]

    因为偶尔会使用ctags执行跳转，这里安装下ctags

    ctags下载链接 [ctags.exe](http://www.vim.org/scripts/download_script.php?src_id=10387)

    下载ctags.exe保存到`%HOMEPATH%\.vim_runtime\plugins_for_me_win\ctags_win\ctags.exe`

    然后把 `%HOMEPATH%\.vim_runtime\plugins_for_me_win\ctags_win` 加入系统的PAHT变量即可

4.  配置`_vimrc`或`.vimrc`

        if has("unix")
            Plugin 'Valloric/YouCompleteMe'
        elsei has("win16") || has("win32")
            " youcompleteme for windows:
            "   https://bitbucket.org/Haroogan/vim-youcompleteme-for-windows/downloads
            "  解压到 ~/.vim_runtime/plugins_for_me_win/<dir> 即可
            call pathogen#infect('~/.vim_runtime/plugins_for_me_win/{}')
        endif

配置完成之后就可以使用Youcompleteme了，在Windows编写文本文件非常的爽快！

### 效果展示

![ycm win shot](/assets/Skills/ycm_win_shot.png)
