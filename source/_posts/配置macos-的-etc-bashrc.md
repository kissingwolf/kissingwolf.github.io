---
title: 配置macos 的/etc/bashrc
date: 2016-12-25 00:26:54
tags: [Mac,bash]
---

更新了macos本地的/etc/bashrc，配置了更加醒目的提示符，并且安装了bash-completion，做个备忘。

```shell
kevinzou@KevindeAir ~
 $ cat /etc/bashrc
function color_my_prompt {
    local __user_and_host="\[\033[01;32m\]\u@\h"
    local __cur_location="\[\033[01;34m\]\w"
    local __git_branch_color="\[\033[31m\]"
    #local __git_branch="\`ruby -e \"print (%x{git branch 2> /dev/null}.grep(/^\*/).first || '').gsub(/^\* (.+)$/, '(\1) ')\"\`"
    local __git_branch='`git branch 2> /dev/null | grep -e ^* | sed -E  s/^\\\\\*\ \(.+\)$/\(\\\\\1\)\ /`'
    local __prompt_tail="\n \[\033[35m\]$"
    local __last_color="\[\033[00m\]"
    export PS1="$__user_and_host $__cur_location $__git_branch_color$__git_branch$__prompt_tail$__last_color "
}
color_my_prompt


if [ -f $(brew --prefix)/etc/bash_completion ] ; then
	. $(brew --prefix)/etc/bash_completion
fi
```

在git目录中显示如下：

```shell
kevinzou@KevindeAir ~/Documents/Github相关/blog.kissingwolf.com (source)
 $
```

