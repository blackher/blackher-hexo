---
title: rsync linux与window下同步文件
date: 2019-09-19 09:47:05
tags:
---

## 需求window文件同步到linux 下

### linux下安装 rsync server

```bash
百度一下 哈哈
```

### window下安装 rsync client

`注意window 下的rsync.exe 与同步的文件放下同一目录下`

#### window 下拉取linux server 文件

```bash
./rsync.exe -vzrtopg name@ip::module ./downloaddir --port=port --password-file=./password.txt
```

#### window 上传到linux server 文件

```bash
./rsync.exe -avz name@ip::module ./uploaddir --port=port --password-file=./password.txt
```

#### window 定时上传linux server 文件

使用window 的计划任务

`计算机->(右击)->管理->任务计划程序`

![计划任务](http://i0.hdslb.com/bfs/archive/e98814eb6dfdc72103ff5c6e71596cf134b4e527.png)

创建计划任务

![创建任务](http://i0.hdslb.com/bfs/archive/d0555df01f8bed41d06a9742ec6be26fec2afaac.png)

##### bat脚本

```bash
f:
cd F:\cw
./rsync.exe -avz name@ip::module ./uploaddir --port=port --password-file=./password.txt
```
