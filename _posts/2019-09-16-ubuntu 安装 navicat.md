---
layout: post
title: "ubuntu 安装 navicat"
date: 2019-10-16
tags: 数据库
---

# ubuntu 安装 navicat

## 乱码解决
```
修改start_navicat
export LANG="zh_CN.UTF-8"
```

修改合适的字体
```
编辑 -> 常规 编辑器 记录
```

## error:1698错误解决

进入以下文件
```
sudo vim /etc/mysql/mysql.conf.d/mysqld.cnf
[mysqlId]加入 -> skip-grant-tables
```

```
service mysql restart //重启mysql
mysql -u root -p //重新进入mysql
```

```
use mysql;

update user set authentication_string=password('mysql'),plugin='mysql_native_password' where user='root';

select user,plugin from user;
```

再次进入mysql
```
service mysql restart
mysql -u root -p
```


最后注释掉之前的输入
```
sudo vim /etc/mysql/mysql.conf.d/mysqld.cnf
```

正常进入mysql
```
mysql -u root -p
```

## 创建navicat图标
```
sudo vim /usr/share/applications/navicat.desktop

[Desktop Entry]
Encoding=UTF-8
Name=Navicat Premium
Comment=The Smarter Way to manage dadabase
Exec=/home/xiao/navicat/start_navicat
Icon=/home/xiao/navicat/navicat.png
Categories=Application;Database;MySQL;navicat
Version=1.0
Type=Application
Terminal=0
```
保存退出。
要保证上述俩路径正确。
```
cp /usr/share/applications/navicat.desktop ~/桌面
```

## navicat破解
首次运行start_navicat时会在home下新建一个.navicatx64的文件夹，删了即可再次试用。
