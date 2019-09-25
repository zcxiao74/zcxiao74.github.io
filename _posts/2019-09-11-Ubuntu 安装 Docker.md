---
layout: post
title: "Docker安装"
date: 2019-09-11
tags: docker  
---
# Ubuntu Docker安装

1.更换国内软件源，推荐中国科技大学的源，稳定速度快（可选）
```
sudo cp /etc/apt/sources.list /etc/apt/sources.list.bak
sudo sed -i 's/archive.ubuntu.com/mirrors.ustc.edu.cn/g' /etc/apt/sources.list
sudo apt update
```

2.安装需要的包
```
sudo apt install apt-transport-https ca-certificates software-properties-common curl
```

3.添加 GPG 密钥，并添加 Docker-ce 软件源，这里还是以中国科技大学的 Docker-ce 源为例
```
curl -fsSL https://mirrors.ustc.edu.cn/docker-ce/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://mirrors.ustc.edu.cn/docker-ce/linux/ubuntu \
$(lsb_release -cs) stable"
```

4.添加成功后更新软件包缓存
```
sudo apt update
```

5.安装 Docker-ce
```
sudo apt install docker-ce
```

6.设置开机自启动并启动 Docker-ce（安装成功后默认已设置并启动，可忽略）
```
sudo systemctl enable docker
sudo systemctl start docker
```

7.测试运行
```
sudo docker run hello-world
```

8.添加当前用户到 docker 用户组，可以不用 sudo 运行 docker（可选）
```
sudo groupadd docker
sudo usermod -aG docker $USER
```

9.测试添加用户组（可选）
```
docker run hello-world
```

# 安装 Docker Compose
1.安装
```
sudo curl -L https://github.com/docker/compose/releases/download/1.21.2/docker-compose-$(uname -s)-$(uname -m) -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
```

2.检验
```
docker-compose -v
```

3.卸载
```
sudo rm /usr/local/bin/docker-compose
```
