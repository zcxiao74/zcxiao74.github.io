---
layout: post
title: "Ubuntu 安装 PostgreSQL"
date: 2019-10-23
tags: 数据库
---

# Ubuntu 安装 PostgreSQL

## 下载安装
```
sudo apt-get update
sudo apt-get install postgresql postgresql-client
```

## 切换到 postgres 用户来开启命令行工具
```
sudo -i -u postgres
```

## 连接到示例数据库( postgres )
```
psql
```

## 退出PostgreSQL 提示符
```
\q
```

## PostgreSQL 安装完成后默认是已经启动的，但是也可以通过下面的方式来手动启动服务
```
sudo /etc/init.d/postgresql start   # 开启
sudo /etc/init.d/postgresql stop    # 关闭
sudo /etc/init.d/postgresql restart # 重启
```
