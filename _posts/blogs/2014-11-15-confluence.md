---
layout:     post
title:      confluence安装手册
category: blogs
tags:         [wiki]
description: wiki是个非常好的文档系统。
---

### 环境准备 
操作系统：Linux

confluence版本：5.4.4

数据库：mysql 5 

### 软件下载 
confluence安装包：[atlassian-confluence-5.4.4-x64_1.bin](https://www.atlassian.com/software/confluence/download)

confluence中文包：[JIRA-Language-STD-CN.jar](http://dl.iteye.com/topics/download/a8e03f06-b333-35cf-9403-90a842c407fa)

confluence破解包：[jira_crack.zip](http://dl.iteye.com/topics/download/2e3ec41d-92aa-348f-9c75-73f10b6fba06)

mysql驱动：[mysql-connector-java-5.1.34-bin.jar ](http://dl.iteye.com/topics/download/7f00832a-b07e-32cb-856f-ce49c545f48a)

### 数据库准备 
创建jiradb数据库 

```mysql
CREATE DATABASE confluence CHARACTER SET utf8 COLLATE utf8_bin;
```

权限用户授权

```mysql
GRANT SELECT,INSERT,UPDATE,DELETE,CREATE,DROP,ALTER,INDEX on confluence.* TO '<db user>'@'<db hostname>' IDENTIFIED BY '<db password>';  
  
flush privileges;  
  
/*  
例如：  
GRANT SELECT,INSERT,UPDATE,DELETE,CREATE,DROP,ALTER,INDEX on confluence.* TO 'root'@'localhost' IDENTIFIED BY '123456';  
*/
```

### 系统环境变量
设置语言为zh_CN，如果语言为en_US则confluence汉化无法生效，最好在.profile文件中配置

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
$ locale  
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

### 安装confluence（使用root用户安装） 
授予执行权限 

```sh
$ chmod +x atlassian-confluence-5.4.4-x64_1.bin
```

安装jira（安装过程中会提示输入相关配置） 

```sh
$ ./atlassian-confluence-5.4.4-x64_1.bin
```

关闭confluence（安装后会自动启动服务） 

```sh
$ service confluence stop
```

### 加载mysql驱动 
拷贝mysql驱动到jira目录/atlassian/confluence/lib

```sh
$ cp mysql-connector-java-5.1.34-bin.jar jira目录/atlassian/confluence/lib/  
```

### 配置confluence 
用浏览器打开confluence的主页面，安装步骤进行配置，其数据库的的配置按照第三步的配置来配置即可。

需要跟jira进行用户整合的请注意（不需的这一步略过），如果你需要跟jira进行结合，那需要注意在jira系统中有一个jira管理员用户是属于jira-system-administrators组，如果没有jira-system-administrators组，则在jira中进行新增并把用户新增到该组。跟jira结合这一步没有配置好，则无法跟jira进行整合。在配置这个一步时，配置有jira-system-administrators组的jira管理员即可。
      
进入界面后，进入插件管理，将中文包插件上传，将提示安装插件成功。重启confluence服务后，中文生效。

```sh
$ service confluence stop  
$ service confluence start
```

### 破解confluence 
将atlassian-extras-2.4.jar包替换掉confluence中的atlassian-extras-2.4.jar，然后重启confluence服务即可。 

### 安装完成 


### 备注 
打开confluence官网忙，下载安装包难，这个原因就不多说了 

生成License比较慢，跟上一个问题一样 