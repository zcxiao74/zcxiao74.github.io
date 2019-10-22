---
layout: post
title: "ubuntu安装maven"
date: 2019-10-22
tags: 工具
---

# ubuntu 安装 maven

## 官网下载
```
https://maven.apache.org/download.cgi
```

## 创建maven目录并解压至此

## 修改全局配置文件
```
sudo vi /etc/profile 
```

添加如下配置:
```
export M2_HOME=/home/xiao/maven
export PATH=${M2_HOME}/bin:$PATH
```

配置生效：
```
source /etc/profile
```

## 检查安装
```
mvn -v
```