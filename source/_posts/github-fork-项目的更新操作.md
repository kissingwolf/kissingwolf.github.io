---
title: github fork 项目的更新操作
date: 2016-12-06 00:23:45
tags: github
---

github上有个很方便的功能叫fork，将别人的工程一键复制到自己账号下。这个功能很方便，但有点不足的是，当源项目更新后，你fork的分支并不会一起更新，需要自己手动去更新。下面为手动更新的方法

1、在本地装好github客户端，或者git客户端

2、clone 自己的fork分支到本地，可以直接使用github客户端，clone到本地，如果使用命令行，命令为：

```
   git clone https://github.com/kissingwolf/UP100_ule.git
```

3、增加源分支地址到你项目远程分支列表中(此处是关键)，先得将原来的仓库指定为upstream，命令为：

```
   git remote add upstream https://github.com/BoobooWei/UP100_ule.git
```

此处可使用git remote -v查看远程分支列表

4、fetch源分支的新版本到本地

```
   [master]> git fetch upstream
```

5、合并两个版本的代码

```
   [master]> git merge upstream/master
```

6、将合并后的代码push到github上去

```
   [master]> git push origin maste
```
