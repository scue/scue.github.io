---
layout: post
title: "VIM学习与配置"
description: ""
category: "技术"
    tags: [VIM]
---

## VIM Map

[Mapping keys in Vim - Tutorial (Part 1)](http://vim.wikia.com/wiki/Mapping_keys_in_Vim_-_Tutorial_(Part_1))

主要有几个Map方法，同时也学习了VIM的这7种模式

    :nmap - Display normal mode maps
    :imap - Display insert mode maps
    :vmap - Display visual and select mode maps
    :smap - Display select mode maps
    :xmap - Display visual mode maps
    :cmap - Display command-line mode maps
    :omap - Display operator pending mode maps

## 分割窗口调整

[Resize splits more quickly](http://vim.wikia.com/wiki/Resize_splits_more_quickly)

*   使用命令行:

        :resize +n  " 横向窗口, n表示数值
        :resize -n  " 横向窗口, n表示数值
        :vertical resize +n " 竖直窗口, n表示数值
        :vertical resize -n " 竖直窗口, n表示数值

*   使用原生快捷键:

        n Ctrl-w +  " 调大窗口，n表示重复次数
        n Ctrl-w -  " 调小窗口，n表示重复次数
        Ctrl-w _    ” 最大化窗口

*   设定快捷键:

        " 我的Leader键是一个‘,’
        " ,+ ,- ,< ,> 分屏时快捷调整大小
        nnoremap <silent> <Leader>+ :exe "resize " . (winheight(0) * 3/2)<CR>
        nnoremap <silent> <Leader>- :exe "resize " . (winheight(0) * 2/3)<CR>
        nnoremap <silent> <Leader>> :exe "vertical resize " . (winwidth(0) * 3/2)<CR>
        nnoremap <silent> <Leader>< :exe "vertical resize " . (winwidth(0) * 2/3)<CR>
