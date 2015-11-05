---
layout:     post
title:      git之https或http方式设置记住用户名和密码的方法
category: blogs
tags:         [git]
description: 在非ssh模式下的git使用，每次都需要输入用户名和密码是不是很烦，这里给大家介绍怎么记住用户名和密码。
---

### 设置记住密码（默认15分钟）

```sh
   git config --global credential.helper cache
```

### 设置记住密码（时间自定义）

```sh
   # 一小时有效期
   git config credential.helper 'cache --timeout=3600'
```

### 设置记住密码（长期有效）

```sh
   git config --global credential.helper store
```
