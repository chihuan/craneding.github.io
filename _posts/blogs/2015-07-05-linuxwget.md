---
layout:     post
title:      Linux wget命令整站下载做网站镜像
category: blogs
description: 强大的wget命令不仅可以断点下载文件，还可以网站整站下载。
---

### 普通下载
简单的下载文件，类似浏览器的文件下载功能。

```sh
$ wget http://www.xxx.com/abc/file.zip
```

### 断点续传
文件大或网络慢不稳定的时候，文件还没下载完成，连接就断开又得重新下载。这个时候可以使用wget的断点续传，只需要在使用的时候加-c参数。

```sh
$ wget -c http://www.xxx.com/abc/file.zip
```

### 批量下载
有多个文件需要下载，那么你只要给wget一个下载清单即可批量下载。编写一个文件，文件的每一行都是需要下载的url地址，然后使用-i参数。

```
# download.txt
http://www.xxx.com/abc/file1.zip
http://www.xxx.com/abc/file2.zip
http://www.xxx.com/abc/file3.zip
```

```sh
$ wget -i download.txt
```

### 选择性下载
可以指定下载某种类型文件，或者不下载某种文件。

```sh
$ wget -m -reiect=gif http://www.xxx.com/abc/

# -reject=gif 表示忽略git文件
# -accept=git 表示下载git文件

```

### 整站下载
可以以递归的方式下载整站，并将下载的页面的链接转换为本地链接，同时可以忽略robots.txt协议和模拟User-Agent。

```sh
$ wget -r -p -np -k -e robots=off -U "Mozilla/5.0 (Macintosh; Intel Mac OS X 10.10; rv:38.0) Gecko/20100101 Firefox/38.0" http://www.xxx.com/abc/

# -r,  --recursive（递归)
# -k,  --convert-links（转换链接）
# -p,  --page-requisites（页面必需元素）
# -np, --no-parent（不追溯至父级）
# -e robots=off, --忽略robots.txt协议
# -U, 模拟User-Agent
```
