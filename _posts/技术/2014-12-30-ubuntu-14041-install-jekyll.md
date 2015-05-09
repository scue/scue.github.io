---
layout: post
title: "Ubuntu 14.04.1 Install Jekyll"
description: ""
category: 技术
tags: [Ubuntu,Jekyll]
---

## RVM安装

如果是个人用户，建议使用RVM，它可以让我们管理Ruby不同版本变得非常方便

相关链接：[RVM实用指南](https://ruby-china.org/wiki/rvm-guide)

## 安装依赖

    sudo apt-get install nodejs libv8-dev

## Jekyll

- 安装`bundler`

        gem install bundler

- 安装`github-pages`

        vi Gemfile
        source 'http://ruby.taobao.org/'
        gem 'github-pages'
        bundle install

	此时，已经可以使用Jekyll命令了；
