# Docker

## 第一章 Docker介绍

### 1.1 docker简介

**Docker**是一个开源的应用容器引擎，让开发者可以打包他们的应用及依赖包到一个可移植的容器中，然后发布到任何流行的**Linux**机器上，也可以实现虚拟化。容器是完全使用沙箱机制，相互之间不会有任何接口。

作为新手，可以简单理解为**Docker**就是轻量级的**VM**虚似机。

### 1.2 Docker是什么？

**Docker**是一个程序运行、测试、交付的开放平台，**Docker**被设计为能够使你快速地交付应用。在**Docker**中，你可以将你的程序分为不同的基础部分，对于每一个基础部分都可以当做一个应用程序来管理。**Docker**能够帮助你快速地测试、快速地编码、快速地交付，并且缩短你从编码到运行应用的周期。

**Docker**使用轻量级的容器虚拟化平台，并且结合工作流和工具，来帮助你管理、部署你的应用程序。

在其核心，**Docker**实现了让几乎任何程序都可以在一个安全、隔离的容器中运行。安全和隔离可以使你可以同时在机器上运行多个容器。

容器轻量级的特性，意味着你可以得到更多的硬件性能。

围绕着容器的虚拟化工具和平台，可以在以下几个方面为你提供帮助：

* 帮助你把应用程序\(包括其余的支持组件\)放入到Docker容器中。
* 分发和转移你的容器至你的团队其它成员来进行进一步的开发和测试。
* 部署这些应用程序至你的生产环境，不论是本地的数据中心还是云平台

### 1.3 Docker企业版和社区版

**Docker**在2017年的3月1号之后，Docker的版本命名开始发生变化，同时将**CE**版本和**EE**版本进行分开。**CE**为社区版本，免费使用，**EE**为企业版本，收费的。

国内公司使用**CentOS**居多，初学者建议直接上手**CentOS**，不同的操作系统，在命令上有细微不同。

* 小知识点：**CentOS**是使用**RedHat**源码编译，因为商标的原因所以命名不同。

![EE和CE版本对比](../assets/docker1.jpeg "EE和CE版本对比")

## 第二章 Docker安装

### 1.Mac安装Docker

##### 1.1 下载Docker for OS X Installer {#11-下载docker-for-os-x-installer}

###### 下载链接[https://docs.docker.com/docker-for-mac/](https://docs.docker.com/docker-for-mac/) {#下载链接httpsdocsdockercomdocker-for-mac}

##### 1.2 安装

将**Docker**拖到**Application**中

然后它会要求你输入密码以获得更高的权限，输入密码即可~~

安装完成！

打开**Docker**后\(如下图所示\)，状态栏中可以看到**Docker**的标志，点开会有“Docker is running”的字样，便可以在终端操作

![](../assets/docker2.png)

### 2.Windows下安装

#### 2.1下载

官网下载boot2docker for windows 1.2

#### 2.2双击打开

需要安装3个部分（如下图所示）

![](../assets/docker3.png)

#### 2.3查看环境变量

安装完成后查看环境变量

**Path**中是否包含**boot2docker**和**Git**

#### 2.4重启电脑

未开启**vt-x**的在**bios**中开启**vt-x**

#### 2.5启动docker

桌面上双击boot2docker start.sh

#### 2.6 等待启动

#### 2.7完成

## 第三章 Docker的主要组成

**Docker**有两个主要的部件：

* Docker: 开源的容器虚拟化平台。
* Docker Hub: 用于分享、管理Docker容器的Docker SaaS平台。

## 第四章 Docker的架构

```
   Docker使用客户端-服务器\(client-server\)架构模式。Docker客户端会与Docker守护进程进行通信。Docker守护 进程会处理复杂繁重的任务，例如建立、运行、发布你的Docker容器。Docker客户端和守护进程可以运行在同一个系统上，当然你也可以使用 Docker客户端去连接一个远程的Docker守护进程。Docker客户端和守护进程之间通过socket或者RESTful API进行通信。

```

![](../assets/docker4.png)

### 4.1Docker守护进程

如上图所示，**Docker**守护进程运行在一台主机上。用不并不直接和守护进程进行交互，而是通过**Docker**客户端间接和其通信。

### 4.2 Docker客户端

**Docker**客户端，实际上是`docker`的二进制程序，是主要的用户与**Docker**交互方式。它接收用户指令并且与背后的**Docker**守护进程通信，如此来回往复。

### 4.3 Docker的内部

要理解**Docker**的内部构建，必须知道以下三种部件：

* Docker镜像 \(Docker images\)。
* Docker仓库 \(Docker registeries\)。
* Docker容器\(Docker containers\)。

#### 4.3.1 Docker镜像

Docker镜像是一个只读的模板。举个例子，一个镜像可以包含一个运行在Apache上的Web应用和其使用的Ubuntu操作系统。

镜像是用来创建容器的。Docker提供了简单的放来来建立新的镜像或者升级现有的镜像，你也可以下载别人已经创建好的镜像。     Docker镜像是Docker的**构造**部分。

* 镜像概念:可以把镜像看做类(java类 JavaScript类)

#### 4.3.2 Docker仓库

Docker仓库用来保存镜像。可以理解为代码控制中的代码仓库。同样的，Docker仓库也有公有和私有的概念。公有的Docker仓库名字是[Docker Hub](http://hub.docker.com/)。Docker Hub提供了庞大的镜像集合供使用。这些镜像可以是你自己创建的，或者你也可以在别人的镜像基础上创建。Docker仓库是Docker的**分发**部分。

#### 4.3.3 Docker容器

Docker容器和文件夹很类似。一个Docker容器包含了所有的某个应用运行所需要的环境。每一个Docker容器都是从Docker镜像创建 的。Docker容器可以运行、开始、停止、移动和删除。每一个Docker容器都是独立和安全的应用平台。Docker容器是Docker的**运行**部分。

* 容器概念:可以把容器看做实例(及new java对象, new JavaScript对象)
* 镜像和容器的关系: Image container = new Image(); 容器是基于镜像创建的

## 第五章 创建Docker应用的详解

### 5.1 ubuntu应用

以**ubuntu**镜像为例： 这个镜像被称为基础镜像，及**Docker**官方提供的（看做它就是个ubuntu的虚拟机）只是一个裸机

以上说了**ubuntu**只是个镜像，我们是不能直接用的，我们最终用到的是容器及"镜像new出来的东西"

### 5.2 搜索镜像

* 首先查看docker的镜像仓库中是否有ubuntu这个镜像

```angular2html
docker search ubuntu
```

```
➜  ~ docker search ubuntu
NAME                                                   DESCRIPTION                                     STARS     OFFICIAL   AUTOMATED
ubuntu                                                 Ubuntu is a Debian-based Linux operating s...   6509      [OK]
dorowu/ubuntu-desktop-lxde-vnc                         Ubuntu with openssh-server and NoVNC            128                  [OK]
rastasheep/ubuntu-sshd                                 Dockerized SSH service, built on top of of...   97                   [OK]
ansible/ubuntu14.04-ansible                            Ubuntu 14.04 LTS with ansible                   86                   [OK]
ubuntu-upstart                                         Upstart is an event-based replacement for ...   77        [OK]
```

* 上图中我们可以看到有我们需要的ubuntu镜像 接下来就把它拉去到本地吧！

### 5.3 拉取镜像

要从docker的镜像仓库中拉去ubuntu这个镜像到本地

```angular2html
docker pull ubuntu
```

```angular2html
➜  ~ docker pull ubuntu
Using default tag: latest
latest: Pulling from library/ubuntu
d5c6f90da05d: Downloading [==========================>                        ]  25.18MB/47.26MB
1300883d87d5: Download complete
c220aa3cfc1b: Download complete
2e9398f099dc: Download complete
dc27a084064f: Download complete
```

### 5.4 查看本地下载镜像

```angular2html
docker images
```

```angular2html
➜  ~ docker images
REPOSITORY                                       TAG                 IMAGE ID            CREATED             SIZE
ubuntu                                           latest              ccc7a11d65b1        3 weeks ago         120MB
mysql/mysql-server                               latest              3157d7f55f8d        5 weeks ago         241MB
registry.cn-hangzhou.aliyuncs.com/haomo/mdexam   zf                  e00964020355        2 months ago        1.64GB
busybox                                          latest              c30178c5239f        2 months ago        1.11MB
juu                                              latest              452596e4f289        2 months ago        118MB
yd/mysql                                         latest              4e84d647f316        3 months ago        586MB
nginx                                            latest              958a7ae9e569        3 months ago        109MB
ubuntu                                           <none>              ebcd9d4fca80        3 months ago        118MB
mysql
```

* 在刚装的情况下应该只显示一个ubuntu镜像 其他镜像是我装的可以忽略

### 5.5 创建第一个容器

```angular2html
docker run -i -t ubuntu /bin/bash
docker run -it --name mdexam --hostname mdexam -d -p - /Users/liuranran/webwork/skilleee:/opt/work \[路径\] /bin/bash
```

```
➜  ~ docker run -i -t ubuntu /bin/bash
root@c6d35db61f33:/# exit
```

* 上面用run命令创建一个给予ubuntu镜像的容器 -i -t参数是调出容器内的shell可以与容器进行交互 exit 退出容器（退出及关闭容器）

### 5.6 查看已启动的容器

```angular2html
docker ps
```

```angular2html
➜  ~ docker ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
```

* docker ps 是查看已启动的容器 加个-a参数查看全部的容器(包括没启动的)

### 5.7 查看所有容器

```angular2html
docker ps -a
```

```angular2html
➜  ~ docker ps -a
查看所有容器

➜  ~ docker ps -a
CONTAINER ID        IMAGE                                               COMMAND                  CREATED             STATUS                      PORTS                               NAMES
3b7409112eb8        ubuntu                                              "/bin/bash"              5 minutes ago       Exited (0) 5 minutes ago                                        sharp_williams
```

* 我们可以看到的信息有这个容器的id(3b7409112eb8) 给予哪个镜像创建的(ubuntu) 还有就是这个容器的名称(sharp_williams)名称是随机分配的

### 5.1 本地下载镜像

/*docker images*/

/*docker ps \(列出所有正在运行的命令\)*/

/*docker run -it --name mdexam --hostname mdexam -d -p - /Users/liuranran/webwork/skilleee:/opt/work \[路径\] /bin/bash*/

docker exec -it centos /bin/bash进入centos

docker commit \[ id\] centos:latest  
docker push centos:latest

docker stop mdexam

docker start mdexam

## 第六章 使用docker可以完成什么？



