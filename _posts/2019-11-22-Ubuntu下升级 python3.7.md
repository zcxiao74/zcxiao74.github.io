---
layout: post
title: "Ubuntu 升级 python3.7.1"
date: 2019-11-22
tags: python  
---

# Ubuntu 升级 python3.7.1

## 下载源码
```
wget https://www.python.org/ftp/python/3.7.1/Python-3.7.1.tgz
```

## 解压源码
```
tar -xvzf Python-3.7.1.tgz
```

## 进入目录
```
cd Python-3.7.1
```

## 配置安装路径
```
./configure --with-ssl --prefix=/usr/local/python3
安装python3.7.1依赖
sudo apt-get update
sudo apt-get install build-essential python-dev python-setuptools python-pip python-smbus libncursesw5-dev libgdbm-dev libc6-dev zlib1g-dev libsqlite3-dev tk-dev libssl-dev openssl libffi-dev
```

## 编译
```
make
```

## 安装
```
sudo make install
```

## 删除软链接
```
sudo rm -rf /usr/bin/python3
sudo rm -rf /usr/bin/pip3
```

## 新建软链接?
```
sudo ln -s /usr/local/python3/bin/python3.7 /usr/bin/python3
sudo ln -s /usr/local/python3/bin/pip3.7 /usr/bin/pip3
```

## 检查
```
python3
```

## 修复安装后无法打开 Terminal 的问题

```
cd /usr/lib/python3/dist-packages/gi/

sudo cp _gi.cpython-35m-x86_64-linux-gnu.so _gi.cpython-37m-x86_64-linux-gnu.so

sudo cp _gi_cairo.cpython-35m-x86_64-linux-gnu.so _gi_cairo.cpython-37m-x86_64-linux-gnu.so
```

```
 \将 gi 模块拷贝到安装路径下的对应目录

sudo cp -r /usr/lib/python3/dist-packages/gi /usr/local/python3/lib/python3.7/site-packages/

``