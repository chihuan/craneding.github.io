---
layout:       post
title:        在Linux系统安装SVN服务器
category:     blogs
tags:         [svn, linux]
description:  怎样在Linux系统上安装SVN服务器呢？怎样能够更好可视化管理SVN呢？
---

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;在Linux系统上安装SVN服务器，随便google或百度一下，数都数不完的教程，基本都是教你怎么下载subversion和apache，接着就安装，安装完就配置apache和subversion，居然连svn的权限和用户名密码等都是纯手工操作的，运气好的时候就非常顺利，运气不好就apache运行不起来，说有错，然后就在网上搜怎么解决，最后给你解决了，可以后就真的这么管理用户名和密码吗？真的是一个大问题啊。

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;还记得以前在旧的公司就是这么干的，基本新来一个开发人员，你就上去自己修改密码文件，基本所有的密码都是一样的，超级不直观，而且就那么几个人会，其它人还不会操作了。这次经过自己两天的学习，终于找到了很好软件解决了这个问题，就是Subversion Edge，下载Subversion Edge后，安装完后就可以用svn了，完成不用你自己安装apache和配置一大堆的东西，而且它还有非常好的web管理界面，超级方便，天啊，以前不知道，真的太落后了。

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Subversion Edge的下载地址是：[http://www.collab.net/downloads/subversion](http://www.collab.net/downloads/subversion)，其官网也有相当详细的安装说明，安装说明基本就搞定，唯一需要注意的是不能用root用户安装，如果用root用户安装的话，是有问题，所以要注意这一点。