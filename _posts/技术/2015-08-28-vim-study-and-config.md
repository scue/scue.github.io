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


## NERDTree的使用

快捷键映射

    """""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""
    " => Nerd Tree
    """""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""
    map <F4> :NERDTreeToggle <CR>
    map <leader>nn :NERDTreeToggle<cr>
    map <leader>nb :NERDTreeFromBookmark
    map <leader>nf :NERDTreeFind<cr>

打开帮助: 输入 `?`

    " NERD tree (4.2.0) quickhelp~
    " ============================
    " File node mappings~
    " double-click,
    " <CR>,
    " o: open in prev window
    " go: preview
    " t: open in new tab
    " T: open in new tab silently
    " middle-click,
    " i: open split
    " gi: preview split
    " s: open vsplit
    " gs: preview vsplit
    "
    " ----------------------------
    " Directory node mappings~
    " double-click, o: open & close node
    " O: recursively open node
    " x: close parent of node
    " X: close all child nodes of current node recursively
    " middle-click, e: explore selected dir
    "
    " ----------------------------
    " Bookmark table mappings~
    " double-click, o: open bookmark
    " t: open in new tab
    " T: open in new tab silently
    " D: delete bookmark
    "
    " ----------------------------
    " Tree navigation mappings~
    " P: go to root
    " p: go to parent
    " K: go to first child
    " J: go to last child
    " <C-j>: go to next sibling
    " <C-k>: go to prev sibling
    "
    " ----------------------------
    " Filesystem mappings~
    " C: change tree root to the selected dir
    " u: move tree root up a dir
    " U: move tree root up a dir but leave old root open
    " r: refresh cursor dir
    " R: refresh current root
    " m: Show menu
    " cd:change the CWD to the selected dir
    " CD:change tree root to CWD
    "
    " ----------------------------
    " Tree filtering mappings~
    " I: hidden files (off)
    " f: file filters (on)
    " F: files (on)
    " B: bookmarks (off)
    "
    " ----------------------------
    " Custom mappings~
    "
    " ----------------------------
    " Other mappings~
    " q: Close the NERDTree window
    " A: Zoom (maximize-minimize) the NERDTree window
    " ?: toggle help
    "
    " ----------------------------
    " Bookmark commands~
    " :Bookmark [<name>]
    " :BookmarkToRoot <name>
    " :RevealBookmark <name>
    " :OpenBookmark <name>
    " :ClearBookmarks [<names>]
    " :ClearAllBookmarks

常用的快捷健:

    ?:      打开帮助
    Enter:  打开文件
    B:      打开书签
    r:      刷新当前目录
    m:      修改当前目录
    cd:     切换到当前目录（主要是为了CtrlP搜索）

关于书签:

存放目录位于`~/.NERDTreeBookmarks`

    cat ~/.NERDTreeBookmarks
    .vim_runtime /home/scue/.vim_runtime
    scue.github.io /docs/work2/github_pages/scue.github.io

如果想要保存书签，在VIM打开NERDTree之后，输入 `:Bookmark [name]` 就可以了

保存书签的名字是可选项，如果没有提供名字，默认是当前路径的basename作为书签名

如果书签里边的路径有误，打开VIM可是会报错的哦，及时清理不用的书签就好了 ;-)
