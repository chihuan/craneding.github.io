---
layout:       post
title:        搭建Oracle数据库的备份服务器
category:     blogs
tags:         [oracle,ssh]
description:  怎样搭建Oracle数据库的备份服务器呢？
---

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;今天终于自己尝试在Ubuntu Server系统上安装了Oracle xe,那下一步就是怎样对oracle数据库的数据进行备份和导入。公司部门的开发环境的数据库服务器没有备份服务器，如果坏了，那且不是麻烦大了，于是我就开始搭建数据库服务器的备份服务器。

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;数据库服务器我们假设为A，数据库备份服务器假设为B，这首先这两台机子都Linux系统和安装Oracle。

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;第一步搭建两台机子可以自动的传输文件（SSH 免密码传输，这样就不需要人工输入密码了）

方法一 

```sh
#在A上的命令:  
    #(连续三次回车,即在本地生成了公钥和私钥,不设置密码)  
    ssh-keygen -t rsa  
    #(需要输入密码)  
    ssh root@172.24.253.2 "mkdir .ssh;chmod 0700 .ssh"  
    #(需要输入密码)  
    scp ~/.ssh/id_rsa.pub B服务器的用户名@B服务器的IP:.ssh/id_rsa.pub   
#在B上的命令:  
    #(如果已经存在这个文件, 跳过这条)  
    touch .ssh/authorized_keys2  
    #(将id_rsa.pub的内容追加到 authorized_keys2 中)  
    cat .ssh/id_rsa.pub >> .ssh/authorized_keys2
```

方法二 

```sh
#在A上的命令:  
    #(连续三次回车,即在本地生成了公钥和私钥,不设置密码)  
    ssh-keygen -t rsa  
    #(需要输入密码)  
    ssh-copy-id -i ~/.ssh/id_rsa.pub "-p ssh端口 B服务器的用户名@B服务器的IP" 
```

第二步备份数据库数据 

数据导出的几种模式 

```sh
    #将数据库db1完全导出,用户名system 密码oracle 导出到/home/oracle/db_backup.dmp中  
      exp system/oracle@db1 file=/home/oracle/db_backup.dmp full=y  
      
    #将数据库中system用户与sys用户的表导出  
      exp system/oracle@db1 file=/home/oracle/db_backup.dmp owner="(system,sys)"  
      
    #将数据库中的表t_table1、t_table2导出  
       exp system/oracle@db1 file=/home/oracle/db_backup.dmp tables="(t_table1,t_table2)"  
      
    #将数据库中的表table1中的字段filed1以"A"结尾的数据导出  
      exp system/oracle@db1 file=/home/oracle/db_backup.dmp tables=(table1) query=" where filed1 like '%A'"  
```

第三步将备份是文件传输到到备份服务器 

```sh
rsync -zva --progress db_backup.dmp B服务器用户名@B服务服务器IP:B服务器的备份路径/db_backup.dmp
```

第四步将数据导入到数据库 

```sh
    imp system/oracle@xe file=daochu.dmp full=y ignore=y  
```

第五步就是写好shell脚本和配Linux的定时任务（脚本就是第一到第三步的内容），使用Linux的crontab来配置定时任务（具体的配置就不详细介绍了），使其能够每天定时备份数据，并把文件备份到另外一台服务器上
第六步是将数据导入到备份数据库服务器的Oracle上，这个步骤暂时不使用定时任务，在需要的时候可以手动导入数据库的数据，而需要注意的是在导入之前，你必须确保你数据库的用户是必须存在的，不然导入的时候会报错，创建数据库的用户如下：

```sql
    create user 用户名 IDENTIFIED BY 密码;  
    GRANT CREATE USER,DROP USER,ALTER USER ,CREATE ANY VIEW ,  
       DROP ANY VIEW,EXP_FULL_DATABASE,IMP_FULL_DATABASE,  
          DBA,CONNECT,RESOURCE,CREATE SESSION TO 用户名字;  
```
