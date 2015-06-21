---
layout:     post
title:      shell执行mysql的SQL语句
category: blog
description: 怎样在脚本中执行myql命令，这或许对定时任务很有作用。
---

### 在脚本中执行mysql的SQL语句

    mysql <<EOF    
      select * from tableA a, tableB b   
      where a.id = b.id;  
    EOF 

