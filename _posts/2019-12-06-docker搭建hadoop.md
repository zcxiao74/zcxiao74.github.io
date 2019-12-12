```
layout: post
title: "docker搭建hadoop"
date: 2019-12-06
tags: hadoop  
```
# docker搭建hadoop

## 配置加速器

```
cd /etc/docker
vim /etc/docker/daemon.json

{"registry-mirrors": ["https://lqbkkmob.mirror.aliyuncs.com"]}

sudo systemctl daemon-reload
sudo systemctl restart docker
```

## 可选项

```
newgrp docker	#更新用户组，获取权限
docker save [id] -o [path/name.tar]	#备份镜像
```

## Docker镜像操作

```
# 远程拉取镜像
docker pull ubuntu

# 在Docker上运行Ubuntu镜像，设置共享目录
docker run -it -v /home/xiao/hadoop:/root/build --name ubuntu ubuntu
$ docker run -it 64613b7ea5bf /bin/bash(单独运行镜像)

# 退出容器并返回
exit / CTRL+P+Q
```

```
这里解析下这个命令参数：
* docker run 表示运行一个镜像；
* -i表示开启交互式；-t表示分配一个tty，可以理解为一个控制台；因此-it可以理解为在当前终端上与docker内部的ubuntu系统交互；
* -v 表示docker内部的ubuntu系统/root/build目录与本地/home/hadoop/build共享；这可以很方便将本地文件上传到Docker内部的Ubuntu系统；
* –name ubuntu 表示Ubuntu镜像启动名称，如果没有指定，那么Docker将会随机分配一个名字；
* ubuntu 表示docker run启动的镜像文件；
```

## Ubuntu系统初始化

```
apt-get update
apt-get install vim
```

安装sshd

```
apt-get install ssh
/etc/init.d/ssh start	# 开启sshd服务器
vim ~/.bashrc
/etc/init.d/ssh start	# 最后一行添加(自启服务)
```

配置sshd

```
ssh-keygen -t rsa #一直按回车键即可
cd ~/.ssh/
cat id_rsa.pub >> authorized_keys
cat authorized_keys		# 查看
ssh localhost	# 验证

vim /etc/ssh/sshd_config

Port 22
PermitRootLogin yes
PubkeyAuthentication yes
PasswordAuthentication yes
ChallengeResponseAuthentication no
UsePAM yes
PrintLastLog no

vim /etc/ssh/ssh_config
StrictHostKeyChecking no(大约35行)
```

安装JDK

```

vim /etc/profile
vim /etc/bash.bashrc

## 最后输入
export JAVA_HOME=/usr/local/jdk1.8
export HADOOP_HOME=/usr/local/hadoop-3.2.1
export JRE_HOME=${JAVA_HOME}/jre
export CLASSPATH=.:${JAVA_HOME}/lib:${JRE_HOME}/lib
export PATH=${JAVA_HOME}/bin:$PATH
export PATH=$PATH:$HADOOP_HOME/bin:$HADOOP_HOME/sbin

source /etc/profile
source /etc/bash.bashrc
```

保存镜像文件

```
https://hub.docker.com	# 注册一个账号
docker login	# 登录，输入用户名密码
docker ps	# 查看当前运行的容器信息
docker commit [ID] ubuntu/jdked	# 保存当前镜像为ubuntu/jdked
docker images	# 检查
```

## 安装Hadoop

```
# 启动镜像
docker run -it -v /home/xiao/hadoop:/root/build --name ubuntu-jdked ubuntu/jdked

# 镜像
docker ps

#进入到运行的容器
docker exec -it 6b97011d772c /bin/bash
docker attach 876d911b2bfb

# 解压hadoop安装包
cd /root/build
tar -zxvf hadoop-3.2.1.tar.gz -C /usr/local

# 配置JAVA_HOME
vim /usr/local/hadoop-3.2.1/etc/hadoop/hadoop-env.sh
export JAVA_HOME=/usr/lib/jvm/java-11-openjdk-amd64/

# 检查
cd /usr/local/hadoop-3.2.1
./bin/hadoop version
```

##　配置Hadoop集群

```
cd /usr/local/hadoop-3.2.1/etc/hadoop
```

设置环境变量

```
vi /etc/profile

export HADOOP_HOME=/usr/local/hadoop-3.2.1
export PATH=$PATH:$HADOOP_HOME/bin

source /etc/profile
```

在/hadoop/sbin路径下：
将start-dfs.sh，stop-dfs.sh两个文件[顶部]添加以下参数

```
#!/usr/bin/env bash
HDFS_DATANODE_USER=root
HADOOP_SECURE_DN_USER=hdfs
HDFS_NAMENODE_USER=root
HDFS_SECONDARYNAMENODE_USER=root
```

start-yarn.sh，stop-yarn.sh[顶部]也需添加以下：

```
#!/usr/bin/env bash
YARN_RESOURCEMANAGER_USER=root
HADOOP_SECURE_DN_USER=yarn
YARN_NODEMANAGER_USER=root
```

vim core-site.xml

```
<configuration>
        <property>
                <name>hadoop.tmp.dir</name>
                <value>file:/usr/local/hadoop-3.2.1/tmp</value>
                <description>namenode上本地的hadoop临时文件夹</description>
      </property>
      <property>
                <name>fs.defaultFS</name>
                <value>hdfs://master:9000</value>
                <description>HDFS的URI，文件系统://namenode标识:端口号</description>
      </property>
</configuration>

```

vim hdfs-site.xml

```
<configuration>
        <property>
                <name>dfs.namenode.name.dir</name>
                <value>file:/usr/local/hadoop-3.2.1/namenode_dir</value>
        </property>
        <property>
                <name>dfs.datanode.data.dir</name>
                <value>file:/usr/local/hadoop-3.2.1/datanode_dir</value>
        </property>
        <property>
                <name>dfs.replication</name>
                <value>3</value>
                <description>副本个数，配置默认是3,应小于datanode机器数量</description>
        </property>
	<property>
		<name>dfs.namenode.http-address</name>
		<value>master:9870</value>
		<description>注意每个节点配置各自的,9870不变</description>
	</property>
</configuration>

```

vim mapred-site.xml

```
<configuration>
	<property>
		<name>mapreduce.framework.name</name>
		<value>yarn</value>
	</property>
</configuration>
```

vim yarn-site.xml

```
<configuration>
	<!--nomenodeManager获取数据的方式是shuffle-->
	<property>
		<name>yarn.nodemanager.aux-services</name>
		<value>mapreduce_shuffle</value>
	</property>
	<!--指定Yarn的老大(ResourceManager)的地址-->
	<property>
		<name>yarn.resourcemanager.hostname</name>
		<value>master</value>
	</property>
</configuration>
```

保存镜像(把容器打包成镜像)

```
sudo docker commit 6b97011d772c ubuntu-hadoop
```

三个终端上分别运行ubuntu-hadoop

```
docker run -it -h master --name master ubuntu-hadoop
docker run -it -h slave01 --name slave01 ubuntu-hadoop
docker run -it -h slave02 --name slave02 ubuntu-hadoop

# 查看容器ip
docker inspect -f '{{.Name}} - {{.NetworkSettings.IPAddress }}' $(docker ps -aq) 

vim /etc/hosts
172.17.0.2      master
172.17.0.3      slave01
172.17.0.4      slave02

# 检测
ssh slave01
ssh slave02

# 备份镜像(可选)
sudo docker commit [id] hadoop-master
sudo docker commit [id] hadoop-slave01
sudo docker commit [id] hadoop-slave02
```

vim /usr/local/hadoop-3.2.1/etc/hadoop/workers (master)

```
# 将localhost替换成两个slave的主机名
slave01
slave02
```

## 启动集群

```
master:
cd /usr/local/hadoop-3.2.1
bin/hdfs namenode -format(格式化)
sbin/start-all.sh

浏览器检查：http://172.17.0.2:9870/
```

##　重启容器后

```
注意容器启动顺序不能乱：
docker start master slave01 slave02

docker attach master
docker attach slave01
docker attach slave02

echo -e "172.17.0.2\\tmaster\\n172.17.0.3\\tslave01\\n172.17.0.4\\tslave02" >> /etc/hosts

/usr/local/hadoop-3.2.1/sbin/start-all.sh
```

