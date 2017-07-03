# Docker培训 {#docker培训}

## 第一章 Docker介绍 {#第一章-docker介绍}

### 1.1 docker简介 {#11-docker简介}

```
Docker 是一个开源的应用容器引擎，让开发者可以打包他们的应用以及依赖包到一个可移植的容器中，然后发布到任何流行的\[Linux\]机器上，也可以实现\[虚拟化\]。容器是完全使用\[沙箱\]机制，相互之间不会有任何接口。

```

### 1.2 Docker是什么？ {#12-docker是什么？}

Docker是一个程序运行、测试、交付的开放平台，Docker被设计为能够使你快速地交付应用。在Docker中，你可以将你的程序分为不同的 基础部分，对于每一个基础部分都可以当做一个应用程序来管理。Docker能够帮助你快速地测试、快速地编码、快速地交付，并且缩短你从编码到运行应用的 周期。

Docker使用轻量级的容器虚拟化平台，并且结合工作流和工具，来帮助你管理、部署你的应用程序。

在其核心，Docker实现了让几乎任何程序都可以在一个安全、隔离的容器中运行。安全和隔离可以使你可以同时在机器上运行多个容器。

容器轻量级的特性，意味着你可以得到更多的硬件性能。

围绕着容器的虚拟化工具和平台，可以在以下几个方面为你提供帮助：

* 帮助你把应用程序\(包括其余的支持组件\)放入到Docker容器中。
* 分发和转移你的容器至你的团队其它成员来进行进一步的开发和测试。
* 部署这些应用程序至你的生产环境，不论是本地的数据中心还是云平台

## 第二章 Docker安装 {#第二章-docker安装}

### 1.mac安装docker {#1mac安装docker}

##### 1.1 下载docker for OS X Installer {#11-下载docker-for-os-x-installer}

###### 下载链接[https://docs.docker.com/docker-for-mac/](https://docs.docker.com/docker-for-mac/) {#下载链接httpsdocsdockercomdocker-for-mac}

##### 1.2 安装 {#12-安装}

将Docker拖到Application中

然后它会要求你输入密码以获得更高的权限，输入密码即可~~

安装完成！

打开docker后\(如下图所示\)，状态栏中可以看到docker的标志，点开会有“Docker is running”的字样，便可以在终端操作![](https://hxgqh.gitbooks.io/haomotraining/content/assets/docker1-1-2.png)

### 2.Windows下安装 {#2windows下安装}

#### 2.1下载 {#21下载}

官网下载boot2docker for windows 1.2

#### 2.2双击打开 {#22双击打开}

需要安装3个部分（如下图所示）

![](https://hxgqh.gitbooks.io/haomotraining/content/assets/docker2-2-2.png)

#### 2.3查看环境变量 {#23查看环境变量}

安装完成后查看环境变量

Path中是否包含boot2docker和git

#### 2.4重启电脑 {#24重启电脑}

未开启vt-x的在bios中开启vt-x

#### 2.5启动docker {#25启动docker}

桌面上双击boot2docker start.sh

#### 2.6 等待启动 {#26-等待启动}

#### 2.7完成 {#27完成}

## 第三章 Docker的主要组成 {#第三章-docker的主要组成}

Docker有两个主要的部件：

* Docker: 开源的容器虚拟化平台。
* Docker Hub: 用于分享、管理Docker容器的Docker SaaS平台。

## 第四章 Docker的架构 {#第四章-docker的架构}

```
   Docker使用客户端-服务器\(client-server\)架构模式。Docker客户端会与Docker守护进程进行通信。Docker守护 进程会处理复杂繁重的任务，例如建立、运行、发布你的Docker容器。Docker客户端和守护进程可以运行在同一个系统上，当然你也可以使用 Docker客户端去连接一个远程的Docker守护进程。Docker客户端和守护进程之间通过socket或者RESTful API进行通信。

```

![](http://static.open-open.com/lib/uploadImg/20141013/20141013170235_453.png)

### 4.1Docker守护进程 {#articleHeader7}

如上图所示，Docker守护进程运行在一台主机上。用不并不直接和守护进程进行交互，而是通过Docker客户端间接和其通信。

### 4.2 Docker客户端 {#articleHeader8}

Docker客户端，实际上是`docker`的二进制程序，是主要的用户与Docker交互方式。它接收用户指令并且与背后的Docker守护进程通信，如此来回往复。

### 4.3 Docker的内部 {#articleHeader9}

要理解Docker的内部构建，必须知道以下三种部件：

* Docker镜像 \(Docker images\)。
* Docker仓库 \(Docker registeries\)。
* Docker容器\(Docker containers\)。

#### 4.3.1 Docker镜像 {#431-docker镜像}

```
   Docker镜像是一个只读的模板。举个例子，一个镜像可以包含一个运行在Apache上的Web应用和其使用的Ubuntu操作系统。

   镜像是用来创建容器的。Docker提供了简单的放来来建立新的镜像或者升级现有的镜像，你也可以下载别人已经创建好的镜像。     Docker镜像是Docker的**构造**部分。

```

#### 4.3.2 Docker仓库 {#432-docker仓库}

```
   Docker仓库用来保存镜像。可以理解为代码控制中的代码仓库。同样的，Docker仓库也有公有和私有的概念。公有的Docker仓库名字是[Docker Hub](http://hub.docker.com/)。Docker Hub提供了庞大的镜像集合供使用。这些镜像可以是你自己创建的，或者你也可以在别人的镜像基础上创建。Docker仓库是Docker的**分发**部分。

```

#### 4.3.3 Docker容器 {#433-docker容器}

```
   Docker容器和文件夹很类似。一个Docker容器包含了所有的某个应用运行所需要的环境。每一个Docker容器都是从Docker镜像创建 的。Docker容器可以运行、开始、停止、移动和删除。每一个Docker容器都是独立和安全的应用平台。Docker容器是Docker的**运行**部分。

```

## 第五章 Docker实际操作 {#第五章--docker实际操作}

### 5.1 本地下载镜像 {#51-本地下载镜像}

docker images

docker ps \(列出所有正在运行的命令\)

docker run -it --name mdexam --hostname mdexam -d -p - /Users/liuranran/webwork/skilleee:/opt/work \[路径\] /bin/bash

docker exec -it centos /bin/bash进入centos

docker commit \[ id\] centos:latest  
docker push centos:latest

docker stop mdexam

docker start mdexam

## 第六章 使用docker可以完成什么？ {#第六章-使用docker可以完成什么？}



