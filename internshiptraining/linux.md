# linux

#### 作者：高天阳
#### 邮箱：13683265113@163.com

```
更改历史

* 2018-09-07	    高天阳	补充最佳实践
* 2017-06-29	    高天阳	初始化文档

```

## 1 文件、目录操作命令

### 1.1 ls命令

* 功能：显示文件和目录的信息

`ls　以默认方式显示当前目录文件列表`  
`ls -a 显示所有文件包括隐藏文件`  
`ls -l 显示文件属性，包括大小，日期，符号连接，是否可读写及是否可执行`  
`ls -lh 显示文件的大小，以容易理解的格式印出文件大小 (例如 1K 234M2G)`  
`ls -lt 显示文件，按照修改时间排序`

### 1.2 cd命令

* 功能：改名目录

`cd dir　切换到当前目录下的dir目录`  
`cd /　切换到根目录`  
`cd ..　切换到到上一级目录`  
`cd ../..　切换到上二级目录`  
`cd ~　切换到用户目录，比如是root用户，则切换到/root下`

### 1.3 cp命令

* 功能：copy文件

`cp source target　将文件source复制为target`  
`cp /root /source.　将/root下的文件source复制到当前目录`  
`cp –av soure_dir target_dir　将整个目录复制，两目录完全一样`

### 1.4 rm命令

* 功能：删除文件或目录

`rm file　删除某一个文件`  
`rm -f file 删除时候不进行提示。可以于r参数配合使用`  
`rm -rf dir　删除当前目录下叫dir的整个目录`

### 1.5 mv命令

* 功能：将文件移动走，或者改名，在uinx下面没有改名的命令，如果想改名，可以使用该命令

`mv source target　将文件source更名为target`

### 1.6 diff

* 功能：比较文件内容

`diff dir1 dir2　比较目录1与目录2的文件列表是否相同，但不比较文件的实际内容，不同则列出`  
`diff file1 file2　比较文件1与文件2的内容是否相同，如果是文本格式的文件，则将不相同的内容显示，如果是二进制代码则只表示两个文件是不同的`  
`comm file1 file2　比较文件，显示两个文件不相同的内容`

### 1.7 ln命令

* 功能：建立链接。windows的快捷方式就是根据链接的原理来做的

`ln source_path target_path 硬连接`  
`ln -s source_path target_path 软连接`

## 2 查看文件内容命令

### 2.1 cat命令

* 显示文件的内容，和DOS的type相同

`cat file`

### 2.2 more命令

* 功能：分页显示命令

`more　file`  
`more命令也可以通过管道符(|)与其他的命令一起使用,例如：`  
`ps ux|more`  
`ls|more`

### 2.3 tail 命令

* 功能：显示文件的最后几行

`tail -n 100 aaa.txt 显示文件aaa.txt文件的最后100行`

### 2.4 vi命令

`vi file　编辑文件file`  
`vi 原基本使用及命令：`  
`输入命令的方式为先按[ESC]键，然后输入:w(写入文件),:w!(不询问方式写入文件）,:wq保存并退出,:q退出,q!不保存退出`

### 2.5 touch命令

* 功能：创建一个空文件

`touch aaa.txt 创建一个空文件，文件名为aaa.txt`

## 3 网络管理

### 3.1 ssh-copy-id命令

`ssh-copy-id`命令可以把本地主机的公钥复制到远程主机的`authorized_keys`文件上，
`ssh-copy-id`命令也会给远程主机的用户主目录（home）和`~/.ssh`, 和`~/.ssh/authorized_keys`设置合适的权限。

语法

``
ssh-copy-id [-i [identity_file]] [user@]machine
``

选项

`-i：指定公钥文件`

实例

1、把本地的ssh公钥文件安装到远程主机对应的账户下：

```
ssh-copy-id root@172.16.78.192
ssh-copy-id -i ~/.ssh/id_rsa.pub root@172.16.78.192
```

## 参考资料:

* [LINUX下常用SHELL指令](http://www.cnblogs.com/nezha/p/3239601.html)
* [linux命令大全](http://man.linuxde.net/par/5)

