---
title: 编写使用LVM快照备份Mysql的脚本
date: 2016-12-08 23:08:39
tags: [mysql,lvm,backup]
---

今天北京的同事问如何编写使用LVM快照备份Mysql的脚本。

想来还是很简单的，主要是有一个坑，mysql 中“LOCK TABLES” 的会话是不能中断的，如果脚本中先执行mysql 锁语句，然后断开连接去执行lvm快照的创建，其实数据库是没有锁住的。

听到这个问题，突然灵光一现，想到其实是多进程问题，要在锁住数据库的同时执行lvm快照创建备份操作。于是写了如下测试代码：

```shell
#!/bin/bash
mkfifo /tmp/mypipo
mysql mydb </tmp/mypipe &
(
  echo "LOCK TABLES mytable READ ;" 1>&6 
  echo "Create LVM snapshot "
  echo "UNLOCK  tables;" 1>&6
) 6> /tmp/myspipe
```

然后有想起来mysql中是有一个SYSTEM指令的，可以执行外部系统命令，就想到了另外一种做法：

```shell
#!/bin/bash
mysql <<ENF
LOCK TABLES mytable READ;
SYSTEM /path/to/create_lvm_snapshot.sh
UNLOCK TABLES;
ENF
```

北京同事选了第二种方法。