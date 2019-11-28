---
layout: post
title: "deepin 安装 python3.8.0"
date: 2019-11-22
tags: python
---

# deepin 安装 python3.8.0

## 下载源码
## 解压源码
## 进入目录
```
cd Python-3.8.0
```

## 配置安装路径
```
sudo ./configure --prefix=/usr/local/python-3.8.0
```

## 编译安装
```
sudo make && sudo make install
```

## 查看默认指向
```
ls -l /usr/bin/python
ls -l /usr/bin/python3
```

## 建立软连接
```
sudo rm -rf python
sudo ln -s /usr/local/python-3.8.0/bin/python3.8 python
```

## 检查
```
python
```
