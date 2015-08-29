---
layout:       post
title:        不翻墙也能更新和管理Android SDK
category:     blogs
description:  Android官网已经打不开了，怎么更新Android SDK呢？不用担心自有解决的方法。  
---

### Android SDK在线更新镜像服务器

1. 中国科学院开源协会镜像站地址:

    IPV4/IPV6: http://mirrors.opencas.cn 端口：80

    IPV4/IPV6: http://mirrors.opencas.org 端口：80
  
    IPV4/IPV6: http://mirrors.opencas.ac.cn 端口：80

2. 上海GDG镜像服务器地址:

    http://sdk.gdgshanghai.com 端口：8000

3. 北京化工大学镜像服务器地址:

    IPv4: http://ubuntu.buct.edu.cn/ 端口：80

    IPv4: http://ubuntu.buct.cn/ 端口：80

    IPv6: http://ubuntu.buct6.edu.cn/ 端口：80

4. 大连东软信息学院镜像服务器地址:

    http://mirrors.neusoft.edu.cn 端口：80
    
使用方法：

1. 启动Android SDK Manager（相关命令：anrorid sdk），打开主界面，依次选择【Tools】、【Options】，弹出【Android SDK Manager - Settings】窗口

2. 在【Android SDK Manager - Settings】窗口中，在【HTTP Proxy Server】和【HTTP Proxy Port】输入框内填入上面镜像服务器地址（不包含http:// ，如下图）和端口，并且选中【Force https://... source to be fetched using http://...】复选框。

3. 依次选择【Packages】、【Reload】。

<img width="40%" height="20%" alt="SDK Manager Proxy Settings" src="http://www.androiddevtools.cn/static/image/sdk-manager-proxy-settings.png">

> 本文参考：[Android Dev Tools官网](http://www.androiddevtools.cn/)



