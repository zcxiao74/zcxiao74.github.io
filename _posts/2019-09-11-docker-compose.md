---
layout: post
title: "docker-compose"
date: 2019-09-11
tags: 容器  
---
# docker-compose

启动应用(后台)
```
docker-compose up
docker-compose up -d
```

列举所有本地镜像
```
docker image ls
```

检查镜像
```
 docker inspect ID/Names
 ```

停止镜像
```
 docker-compose down
```

查看当前运行的应用
```
docker-compose ps
```

查看所有可用的命令
```
docker-compose --help
```

停止服务
```
docker-compose stop
```

移除容器
```
docker-compose down --volumes
```
