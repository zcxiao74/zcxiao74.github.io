```
layout: post
title: "deepin 安装 docker-ce"
date: 2019-12-04
tags: docker
```

# deepin 安装 docker-ce

## 先卸载
```
sudo apt-get remove docker docker-engine docker.io
```
## 安装依赖

```
sudo apt-get install apt-transport-https ca-certificates curl gnupg2 software-properties-common
```

## 信任 Docker 的 GPG 公钥: 

```
curl -fsSL https://download.docker.com/linux/debian/gpg | sudo apt-key add -
```

## 安装

```
sudo apt-get update
sudo apt-get install docker-ce
```

## 给予权限(不需要每次都sudo)

```
#添加docker用户组
sudo groupadd docker

#将登陆用户加入到docker用户组中
sudo gpasswd -a $USER docker

#更新用户组
newgrp docker

#测试docker命令是否可以使用sudo正常使用
docker ps
```

