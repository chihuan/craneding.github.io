---
layout:       post
title:        在RedHat 5上安装Oracle
category:     blogs
tags:         [oracle, linux]
description:  安装Oracle那是相当麻烦，特别是系统太新或系统旧的情况下会有很多奇怪问题。
---

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;最近自己动手安装了Oracle，看了网上很多的教程，很都是说的不清不楚的，有的甚至有点误导，让你感觉是超级的麻烦。其实也没那么麻烦，在网上也找到了一篇写的不错的教程，地址：[http://www.cnblogs.com/edwardcmh/archive/2012/11/30/2796559.html](http://www.cnblogs.com/edwardcmh/archive/2012/11/30/2796559.html)，不过博客中的3-6这四个步骤我是没有做的，就直接跳过到第七个步骤开始了。

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;安装完了Oracle，测试通过了，不过Oracle是没有设置开机启动的，也就是说你重启了电脑了之后，就得自己手动的启动数据库，这也是比较繁琐的操作，这也找到了一个很好的教程，地址：[http://www.cnblogs.com/edwardcmh/archive/2012/05/11/2495671.html](http://www.cnblogs.com/edwardcmh/archive/2012/05/11/2495671.html)或[http://www.oracle-base.com/articles/linux/automating-database-startup-and-shutdown-on-linux.php](http://www.oracle-base.com/articles/linux/automating-database-startup-and-shutdown-on-linux.php)按照这篇文章，基本就搞定了Oracle的安装和自动启动。