---
layout: post
title: "Ubuntu 18.04下使用Apache搭建一个web服务器"
date: 2019-09-26
tags: apache
---
# Ubuntu 18.04下使用Apache搭建一个web服务器

## apache 安装
```
sudo apt install apache2 -y
```

检查
```
systemctl status apache2
```

常用命令
```
/etc/init.d/apache2 start    //启动Apache服务
/etc/init.d/apache2 stop    //停止Apache服务
/etc/init.d/apache2 restart    //重启Apache服务
```

默认根目录(修改后重启)： /etc/apache2/sites-available/000-default.conf
默认html位置：/var/www/html
默认网页：/etc/apache2/mods-available/dir.conf

##报错Server unable to read htaccess file, denying access to be safe
您没有访问此资源的权限。服务器无法读取htaccess文件，拒绝安全访问
根目录下新建“.htaccess”文件，写入：
```
Order allow,deny
Allow from all
Require all granted
```
再将目录设置为可执行
```
chmod -R 755 /home/xiao/apache
```
同时修改apache配置文件中Directory节点，
/etc/apache2/apache2.conf大致如下：
```
<Directory "/home/fynas/www">
    Options FollowSymLinks
    AllowOverride all
    Require all granted #新版本apache变成这样的
</Directory>
```

## apache 卸载

删除apache
```
$ sudo apt-get --purge remove apache2
```

找到没有删除掉的配置文件，一并删除
```
$ sudo find /etc -name "*apache*" |xargs  rm -rf
$ sudo rm -rf /var/www
$sudo rm -rf /etc/libapache2-mod-jk
 ```

删除关联，这样就可以再次用apt-get install apache2 重装了
```
dpkg -l |grep apache2|awk '{print $2}'|xargs dpkg -P
```

## 安装php环境
```
sudo apt-get install php7.0
php -v

sudo apt-get install libapache2-mod-php7.0
sudo apt-get install php7.0-gd
```

## 检验php
```
cd /var/www/html
sudo vim test.php

<?php
	phpinfo();
?>

保存后浏览器访问：localhost/test.php
```

## 安装mysql-php插件
```
mysql -V
sudo apt-get install php7.0-mysql
sudo apt-get install composer
composer
```
