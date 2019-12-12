---
layout: post
title: "ubuntu 安装 mysql"
date: 2019-10-21
tags: 数据库
---

# ubuntu 安装 mysql

## 安装MySQL
```
sudo apt-get install mysql-server mysql-client
```

## 检查mysql是不是在运行
```
sudo service mysql status
```

## 一般安装完成之后都是会自动运行的，如果没有运行可以start
```
sudo service mysql start
```

## 访问数据库
```
sudo mysql -uroot -p
```

## 卸载
```
sudo apt purge mysql-*
sudo rm -rf /etc/mysql/ /var/lib/mysql
sudo apt autoremove
```

## 修改密码

```
mysql -u root -p
use mysql;
update user set authentication_string=PASSWORD("mysql") where user='root';
flush privileges;
quit;
/etc/init.d/mysql restart;
```



