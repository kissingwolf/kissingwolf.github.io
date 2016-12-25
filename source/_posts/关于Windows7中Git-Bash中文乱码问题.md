---
title: 关于Windows7中Git Bash中文乱码问题
date: 2016-12-25 22:45:11
tags: [git,windows,中文化]
---

今天和同事小龙在其Windows 7 的笔记本电脑上配置GitHub Blog的时候，发现Windows 7 下的Git Bash环境下中文字符显示为乱码，并且无法正常输入中文。

晚上查了一下手册，发现是Windows 7环境下字符编码问题。

> 提交时字符编码问题

打开Git Bash终端，在`~`目录下修改`.gitconfig`文件内容，如果没有这个文件就建一个。

添加内容如下：

```config
[gui] 
encoding = utf-8 
[i18n] 
commitencoding = GB2312 #log编码，window 7下默认编码为gb2312,声明后发到GitHub服务器才不会乱码 
[svn] 
pathnameencoding = GB2312 #支持中文路径
```

> 显示目录信息时字符编码问题

在`/etc/profile.d/aliases.sh`文件中确认如下内容是否存在，如果不存在或是被注释了，请修改：

```config
alias ls='ls --show-control-chars --color=auto' #ls能够正常显示中文
```

> 输入时字符编码问题

在`/etc`目录下找到`inputrc`文件，确认如下两行是否存在，如果不存在请添加，如果被注释请取消注释：

```config
set output-meta on #可以正常输入中文 
set convert-meta off

```

**Windows 10 Git Bash 安装后可以正常显示中文，无需做任何调整**

