---
layout:     post
title:      nginx平滑升级
category: blogs
description: nginx怎样在不停机的情况下进行升级呢？
---

### 重命名主进程文件
 旧版本 nginx 的主进程将重命名它的 pid 文件为 .oldbin(例如：/usr/local/nginx/logs/nginx.pid.oldbin) 

```sh
$ kill -USR2 【旧颁布的Nginx主进程号】  
```

### 同时运行nginx
 新、旧版本的nginx 实例会同时运行，共同处理输入的请求。要逐步停止旧版本的 nginx 实例，你必须发送 WINCH 信号给旧的主进程，然后，它的工作进程就将开始从容关闭 

```sh
$ kill -WINCH 【旧版本的Nginx主进程号】
```

### 升级或恢复
 可以决定是使用新版本，还是恢复到旧版本 

```sh
$ kill 【新的主进程号或旧的主进程号】
```
