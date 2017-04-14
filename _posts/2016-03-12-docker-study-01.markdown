---
layout: single
title: "Docker学习01"
date: 2016-03-12 20:19:16 +0800
comments: true
categories: 
---
# Docker基本情况 #

## 隔离 ##

- 文件系统
- 进程
- 网络
- 资源隔离与分组，通过cgroups

## 数据卷 ##

可以方便的用于文件共享；只读挂载可以方便的放置 **FLAG**。

```sh
docker run -v /data:/datavolume:ro
```
数据卷容器可以方便地实现多个容器之间的数据共享。

```sh
docker run --volumes-from CNAME
```

## 常用命令 ##

### 容器控制 ###

- docker run：运行
- Ctrl-P Ctrl-Q： 退出挂载
- docker attach：挂载
- docker start：启动容器，可以使用 **-i** 选项
- docker exec：在运行的容器中执行命令
- docker stop：停止容器，实际就是发送Ctrl-C
- docker kill：停止容器，直接终止进程

## 构建Docker镜像 ##

- docker commit
- Dockerfile

### Dockerfile ###

思路值得借鉴，从一个现有基础镜像出发，根据配置文件自动化地生成新的镜像。但是Windows有些软件安装和配置如何从命令行完成需要进一步探索。

## Docker网络连接 ##

### 基于Linux网桥 ###

类似于VMware Workstation中的HostOnly模式，允许主机、虚拟机之间通信。

```sh
apt-get install bridge-utils
brctl add br0
ifconfig br0 192.168.xx.1/24
echo 'DOCKER_OPTS="-b br0"' >> /etc/default/docker
service docker restart
```

有个问题需要注意：每次启动的时候，虚拟机的IP地址都可能不一样。但是可以通过`--link=cname:alias`来指定主机内部别名。

### 通过iptables控制容器间网络连接 ###

通过`--icc=false --iptables=true`启用，在DOCKER规则链中控制容器间连接。通过`--link`选项确定哪些容器之间可以连接。

### 与外部网络的连接 ###

查看IP转发是否开启：

```sh
sudo sysctl net.ipv4.conf.all.forwarding
```

通过iptables限制外部对容器的访问，例如：

```sh
iptables -I DOCKER -s src_ip -d dst_ip -p TCP --dport 80 -j DROP
```

### 使用Open vSwitch实现跨服务器连接 ###

创建Open vSwitch接口，然后挂载到bridge上。

## 搭建Docker私有Registry ##



## 实例 ##

### 创建Web站点 ###

创建导出80端口的容器：

```sh
docker run -p 80 --name web -it ubuntu /bin/bash
```

安装nginx、vim；编辑nginx配置；创建网页文件；运行nginx。
