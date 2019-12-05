```
layout: post
title: "deepin安装jdk及永久配置方法"
date: 2019-12-04
tags: java  
```

# deepin安装jdk及永久配置方法

## 解压安装

## 修改配置文件

```
sudo vim /etc/profile
sudo vim /etc/bash.bashrc
```

## 最后写入

```
JAVA_HOME=/home/xiao/develop/jdk1.8.0
CLASSPATH=.:$JAVA_HOME/bin.tools.jar
PATH=$JAVA_HOME/bin:$PATH
export JAVA_HOME CLASSPATH PATH
```

## 生效

```
source /etc/profile
source /etc/bash.bashrc
```

