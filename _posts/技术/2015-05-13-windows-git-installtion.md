---
layout: post
title: "Windows Git安装和配置"
description: ""
category: 技术
tags: [Windows]
---

### 安装Git客户端

目前有两个客户端可以选择

-   [Git-1.9.5-preview20150319.exe](https://www.git-scm.com/download/win)
-   [GithubSetup.sexe](https://github-windows.s3.amazonaws.com/GitHubSetup.exe)

我比较推荐使用第一个客户端，当然，同时使用两个客户端也是没有问题的；

安装过程就是一直按一步即可

### 配置Git客户端

1.  先来配置密钥，使用`ssh-keygen`

        ssh-keygen -t rsa -C "scue@vip.qq.com"

2.  配置Windows的`~/.bashrc`和`~/.bash_aliases.git`以加快Windows上的Git操作

    2.1 配置`~/.bashrc`

        function _gmto()
        {
            local cur prev opts
            COMPREPLY=()
            cur="${COMP_WORDS[COMP_CWORD]}"
            prev="${COMP_WORDS[COMP_CWORD-1]}"

            COMPREPLY=( $(compgen -W "$(git branch | sed '/\*/d' | xargs echo)" -- ${cur}) )
            return 0
        }
        case $SHELL in
            '/bin/bash' )
                complete -F _gmto gmto
                ;;
            '/bin/zsh' )
                compdef gmto=git-branch
                ;;
        esac

        # git merge to branch
        gmto(){
            local oldbranch=$(current_branch)
            local mergeto=$1
            git checkout $mergeto
            git merge $oldbranch
            git checkout $oldbranch
        }

        test -e ~/.bash_aliases.git && . ~/.bash_aliases.git

    2.2 配置`~/.bash_aliases.git`

        # Aliases
        alias g='git'
        alias gst='git status'
        alias gd='git diff'
        alias gdc='git diff --cached'
        alias gl='git pull'
        alias gup='git pull --rebase'
        alias gp='git push'
        alias gd='git diff'
        alias gc='git commit -v'
        alias gc!='git commit -v --amend'
        alias gca='git commit -v -a'
        alias gca!='git commit -v -a --amend'
        alias gcmsg='git commit -m'
        alias gco='git checkout'
        alias gcm='git checkout master'
        alias gr='git remote'
        alias grv='git remote -v'
        alias grmv='git remote rename'
        alias grrm='git remote remove'
        alias grset='git remote set-url'
        alias grup='git remote update'
        alias grbi='git rebase -i'
        alias grbc='git rebase --continue'
        alias grba='git rebase --abort'
        alias gb='git branch'
        alias gba='git branch -a'
        alias gcount='git shortlog -sn'
        alias gcl='git config --list'
        alias gcp='git cherry-pick'
        alias glg='git log --stat --max-count=10'
        alias glgg='git log --graph --max-count=10'
        alias glgga='git log --graph --decorate --all'
        alias glo='git log --oneline --decorate --color'
        alias glog='git log --oneline --decorate --color --graph'
        alias gss='git status -s'
        alias ga='git add'
        alias gm='git merge'
        alias grh='git reset HEAD'
        alias grhh='git reset HEAD --hard'
        alias gclean='git reset --hard && git clean -dfx'
        alias gwc='git whatchanged -p --abbrev-commit --pretty=medium'
        
        #remove the gf alias
        #alias gf='git ls-files | grep'
        
        alias gpoat='git push origin --all && git push origin --tags'
        alias gmt='git mergetool --no-prompt'
        
        alias gg='git gui citool'
        alias gga='git gui citool --amend'
        alias gk='gitk --all --branches'
        
        alias gsts='git stash show --text'
        alias gsta='git stash'
        alias gstp='git stash pop'
        alias gstd='git stash drop'
        
        # Will cd into the top of the current repository
        # or submodule.
        alias grt='cd $(git rev-parse --show-toplevel || echo ".")'
        
        # Git and svn mix
        alias git-svn-dcommit-push='git svn dcommit && git push github master:svntrunk'
        
        alias gsr='git svn rebase'
        alias gsd='git svn dcommit'
        #
        # Will return the current branch name
        # Usage example: git pull origin $(current_branch)
        #
        function current_branch() {
          ref=$(git symbolic-ref HEAD 2> /dev/null) || \
          ref=$(git rev-parse --short HEAD 2> /dev/null) || return
          echo ${ref#refs/heads/}
        }
        
        function current_repository() {
          ref=$(git symbolic-ref HEAD 2> /dev/null) || \
          ref=$(git rev-parse --short HEAD 2> /dev/null) || return
          echo $(git remote -v | cut -d':' -f 2)
        }
        
        # these aliases take advantage of the previous function
        alias ggpull='git pull origin $(current_branch)'
        alias ggpur='git pull --rebase origin $(current_branch)'
        alias ggpush='git push origin $(current_branch)'
        alias ggpnp='git pull origin $(current_branch) && git push origin $(current_branch)'
        
        # these alias ignore changes to file
        alias gignore='git update-index --assume-unchanged'
        alias gunignore='git update-index --no-assume-unchanged'
        # list temporarily ignored files
        alias gignored='git ls-files -v | grep "^[[:lower:]]"'

配置好之后，使用Git就变得很爽快
