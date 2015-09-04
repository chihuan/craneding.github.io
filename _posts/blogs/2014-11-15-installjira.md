---
layout:       post
title:        Jira安装手册
category:     blogs
tags:         [jira]
description:  抽点时间写写Jira的安装教程。
---

### 环境准备

操作系统：Linux

Jira版本：6.3.10

数据库：mysql 5 

### 软件下载

Jira安装包：[atlassian-jira-6.3.10-x64.bin](https://www.atlassian.com/zh/software/jira/download?os=linux)

Jira中文包：[JIRA-Language-STD-CN.jar](http://dl.iteye.com/topics/download/afa5f74e-cae3-3934-a7e0-e8ec0d5ecc6a)

Jira破解包：[jira_crack.zip](http://dl.iteye.com/topics/download/dced96f9-5bde-3ab5-8d98-2cdcb9ebee56)

mysql驱动：[mysql-connector-java-5.1.34-bin.jar](http://dl.iteye.com/topics/download/b215ba11-bc4e-3519-ae70-68fe89c2da9e)


### 数据库准备

创建jiradb数据库 

```sql
    CREATE DATABASE jiradb CHARACTER SET utf8 COLLATE utf8_bin;  
```

权限用户授权 

```sql
    GRANT SELECT,INSERT,UPDATE,DELETE,CREATE,DROP,ALTER,INDEX on jiradb.* TO '<db user>'@'<db hostname>' IDENTIFIED BY '<db password>';  
      
    flush privileges;  
      
    /*  
    例如：  
    GRANT SELECT,INSERT,UPDATE,DELETE,CREATE,DROP,ALTER,INDEX on jiradb.* TO 'root'@'localhost' IDENTIFIED BY '123456';  
    */  
```

### 系统环境变量

设置语言为zh_CN，如果语言为en_US则Jira汉化无法生效，最好在.profile文件中配置

在~/.profile文件最后加以下两行

```sh
export LANG=zh_CN.UTF-8  
export LANGUAGE=zh_CN:zh
```

重新加载环境变量（在命令行中输入） 

```sh
source ~/.profile 
```

查看locale 

```sh
    > locale  
    LANG=zh_CN.UTF-8  
    LANGUAGE=zh_CN:zh  
    LC_CTYPE="zh_CN.UTF-8"  
    LC_NUMERIC="zh_CN.UTF-8"  
    LC_TIME="zh_CN.UTF-8"  
    LC_COLLATE="zh_CN.UTF-8"  
    LC_MONETARY="zh_CN.UTF-8"  
    LC_MESSAGES="zh_CN.UTF-8"  
    LC_PAPER="zh_CN.UTF-8"  
    LC_NAME="zh_CN.UTF-8"  
    LC_ADDRESS="zh_CN.UTF-8"  
    LC_TELEPHONE="zh_CN.UTF-8"  
    LC_MEASUREMENT="zh_CN.UTF-8"  
    LC_IDENTIFICATION="zh_CN.UTF-8"  
    LC_ALL=  
```

### 安装jira（使用root用户安装）

授予执行权限

```sh
    > chmod +x atlassian-jira-6.3.10-x64.bin  
```

安装jira（安装过程中会提示输入相关配置） 

```sh
	> ./atlassian-jira-6.3.10-x64.bin 
```

关闭jira（安装后会自动启动服务）

```sh
	> service jira stop
```


### 加载mysql驱动 

拷贝mysql驱动到jira目录/atlassian/jira/lib 

```sh
	> cp mysql-connector-java-5.1.34-bin.jar jira目录/atlassian/jira/lib/
```

### 配置Jira

用浏览器打开Jira的主页面，安装步骤进行配置，其数据库的的配置按照第三步的配置来配置即可，配置完后即可进入界面。

进入界面后，进入插件管理，将中文包插件上传，将提示安装插件成功。重启jira服务后，中文生效。

```sh
    > service jira stop  
    > service jira start  
```

### 破解Jira

解压jira_crack.zip后，有4个文件，两个破解jar包，两个说明文件，请安装说明文件操作，这里就不细说。 


### 安装完成


### 备注

打开jira官网忙，下载安装包难，这个原因就不多说了

生成License比较慢，跟上一个问题一样 