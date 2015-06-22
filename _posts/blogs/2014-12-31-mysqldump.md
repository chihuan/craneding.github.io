---
layout:     post
title:      mysqldump命令的用法
category: blogs
description: 学会使用mysqldump命令进行数据结构和数据的导出。
---

### 导出表结构不导出数据 

    $ mysqldump -d -uusername -hhostname -p dbname > tables.sql

### 导出表结构不导出数据 

    $ mysqldump -t -uusername -hhostname -p dbname > datas.sql

