# rsync

#### 作者：高天阳
#### 邮箱：13683265113@163.com

```
更改历史

* 2018-8-30	    高天阳	初始化文档

```

## 1 简介

### 1.1 简介

rsync是linux系统下的数据镜像备份工具。使用快速增量备份工具Remote Sync可以远程同步，
支持本地复制，或者与其他SSH、rsync主机同步。

### 1.2 特点

可以镜像保存整个目录树和文件系统。

可以很容易做到保持原来文件的权限、时间、软硬链接等等。

无须特殊权限即可安装。

快速：第一次同步时 rsync 会复制全部内容，但在下一次只传输修改过的文件。
rsync 在传输数据的过程中可以实行压缩及解压缩操作，因此可以使用更少的带宽。

安全：可以使用scp、ssh等方式来传输文件，当然也可以通过直接的socket连接。

支持匿名传输，以方便进行网站镜象。

## 2 安装和使用

### 2.1 安装

Ubuntu安装: 

```
sudo apt-get install rsync
```
RedHat: 

```
yum install rsync
```

编译安装
rsync的编译安装非常简单，只需要以下简单的几步：

```
[root@www rsync-2.4.6]# ./configure
[root@www rsync-2.4.6]# make
[root@www rsync-2.4.6]# make install
```

但是需要注意的是必须在服务器A和B上都安装rsync，其中A服务器上是以服务器模式运行rsync，而B上则以客户端方式运行rsync。
这样在web服务器A上运行rsync守护进程，在B上定时运行客户程序来备份web服务器A上需要备份的内容。

### 2.2 使用

#### 2.2.1 服务器端启动

```
usr/bin/rsync --daemon --config=/etc/rsyncd/rsyncd.conf
```

可能需要root权限运行.

`/etc/rsyncd/rsyncd.conf`是你刚才编辑的`rsyncd.conf`的位置.

也可以在`/etc/rc.d/rc.local`里加入让系统自动启动等.

#### 2.2.2 客户端同步

rsync -参数 用户名@同步服务器的IP::rsyncd.conf中那个方括号里的内容 本地存放路径 如:

rsync -avzP nemo@192.168.10.1::nemo /backup

说明：

- -a 参数，相当于-rlptgoD，-r 是递归 -l 是链接文件，意思是拷贝链接文件；-p 表示保持文件原有权限；-t 保持文件原有时间；-g 保持文件原有用户组；-o 保持文件原有属主；-D 相当于块设备文件；
- -z 传输时压缩；
- -P 传输进度；
- -v 传输时的进度等信息，和-P有点关系，自己试试。可以看文档；

#### 2.2.3 参数详解

-v, --verbose 详细模式输出

-q, --quiet 精简输出模式

-c, --checksum 打开校验开关，强制对文件传输进行校验

-a, --archive 归档模式，表示以递归方式传输文件，并保持所有文件属性，等于-rlptgoD

-r, --recursive 对子目录以递归模式处理

-R, --relative 使用相对路径信息

-b, --backup 创建备份，也就是对于目的已经存在有同样的文件名时，将老的文件重新命名为~filename。可以使用--suffix选项来指定不同的备份文件前缀。

--backup-dir 将备份文件(如~filename)存放在在目录下。

-suffix=SUFFIX 定义备份文件前缀

-u, --update 仅仅进行更新，也就是跳过所有已经存在于DST，并且文件时间晚于要备份的文件。(不覆盖更新的文件)

-l, --links 保留软链结

-L, --copy-links 像对待常规文件一样处理软链接

--copy-unsafe-links 仅仅拷贝指向SRC路径目录树以外的链接

--safe-links 忽略指向SRC路径目录树以外的链接

-H, --hard-links 保留硬链接

-p, --perms 保持文件权限

-o, --owner 保持文件属主信息

-g, --group 保持文件属组信息

-D, --devices 保持设备文件信息

-t, --times 保持文件时间信息

-S, --sparse 对稀疏文件进行特殊处理以节省DST的空间

-n, --dry-run显示哪些文件将被传输

-W, --whole-file 拷贝文件，不进行增量检测

-x, --one-file-system 不要跨越文件系统边界

-B, --block-size=SIZE 检验算法使用的块尺寸，默认是700字节

-e, --rsh=COMMAND 指定使用rsh、ssh方式进行数据同步

--rsync-path=PATH 指定远程服务器上的rsync命令所在路径信息

-C, --cvs-exclude 使用和CVS一样的方法自动忽略文件，用来排除那些不希望传输的文件

--existing 仅仅更新那些已经存在于DST的文件，而不备份那些新创建的文件

--delete 删除那些DST中SRC没有的文件

--delete-excluded 同样删除接收端那些被该选项指定排除的文件

--delete-after 传输结束以后再删除

--ignore-errors 即使出现IO错误也进行删除

--max-delete=NUM 最多删除NUM个文件

--partial 保留那些因故没有完全传输的文件，以是加快随后的再次传输

--force 强制删除目录，即使不为空

--numeric-ids 不将数字的用户和组ID匹配为用户名和组名

--timeout=TIME IP超时时间，单位为秒

-I, --ignore-times 不跳过那些有同样的时间和长度的文件

--size-only 当决定是否要备份文件时，仅仅察看文件大小而不考虑文件时间

--modify-window=NUM 决定文件是否时间相同时使用的时间戳窗口，默认为0

-T --temp-dir=DIR 在DIR中创建临时文件

--compare-dest=DIR 同样比较DIR中的文件来决定是否需要备份

-P 等同于 --partial

--progress 显示备份过程

-z, --compress 对备份的文件在传输时进行压缩处理

--exclude=PATTERN 指定排除不需要传输的文件模式

--include=PATTERN 指定不排除而需要传输的文件模式

--exclude-from=FILE 排除FILE中指定模式的文件

--include-from=FILE 不排除FILE指定模式匹配的文件

--version 打印版本信息

--address 绑定到特定的地址

--config=FILE 指定其他的配置文件，不使用默认的rsyncd.conf文件

--port=PORT 指定其他的rsync服务端口

--blocking-io 对远程shell使用阻塞IO

-stats 给出某些文件的传输状态

--progress 在传输时现实传输过程

--log-format=formAT 指定日志文件格式

--password-file=FILE 从FILE中得到密码

--bwlimit=KBPS 限制I/O带宽，KBytes per second

-h, --help 显示帮助信息

### 2.3 示例

### 2.4 最佳实践

## 3 同类型技术比较

## 参考资料

* [rsync百度百科](https://baike.baidu.com/item/rsync/80863389)