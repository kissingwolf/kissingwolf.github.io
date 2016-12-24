---
title: 修改grub2默认启动项目
date: 2016-12-06 23:19:04
tags: [grub2,boot,linux]
---

```shell
[root@rhel7 ~]# grep ^menuentry /boot/gru2/grub.cfg  | curt -f 2 -d \' | nl -v 0
    0 RedHat Enterprise Linux (3.10.12.ooxx) 7 
    1 RedHat Enterprise Linux (4.4.12.ooxx) 7 

[root@rhel7 ~]# grub2-set-default 1
```
