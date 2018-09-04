### 课堂笔记

Linux分不同版本？

Gitadd添加至缓存区

Gitstatus工作区状态

Gitdiff查看不同

回退

Gitlog获取提交id

Gitreset--hardcommit\_id回退至某个版本commit\_id每一次提交会有唯一的id码

Gitcommit提交至缓存区

Gitreflog查看本地指针指向历史

Gitceckout--相对于当前目录的文件名路径撤销修改

Gittag版本标签

Gulp

Srcdesttaskwatch

# Git培训 {#git培训}

## 第一章 Git介绍 {#第一章-git介绍}

### 1.1 Git介绍 {#11-git介绍}

Git是一款分布式版本控制系统。与之对应的是集中式版本控制系统（SVN）。  
那相对于集中式版本控制系统，他有什么优点呢？

### 1.1 Git历史 {#11-git历史}

Linus在1991年创建了开源的Linux，从此，Linux系统不断发展，已经成为最大的服务器系统软件了。 Linus虽然创建了Linux，但Linux的壮大是靠全世界热心的志愿者参与的，这么多人在世界各地为Linux编写代码，那Linux的代码是如何管理的呢？

事实是，在2002年以前，世界各地的志愿者把源代码文件通过diff的方式发给Linus，然后由Linus本人通过手工方式合并代码！

到2002年，linux采用商业化的BitKeeper，BitKeeper的东家BitMover公司出于人道主义精神，授权Linux社区免费使用这个版本控制系统。

到2005年，开发Samba的Andrew试图破解BitKeeper的协议（这么干的其实也不只他一个），被BitMover公司发现了（监控工作做得不错！），于是BitMover公司怒了，要收回Linux社区的免费使用权。

Linus花了两周时间自己用C写了一个分布式版本控制系统，这就是Git！一个月之内，Linux系统的源码已经由Git管理了！

Git迅速成为最流行的分布式版本控制系统，尤其是2008年，GitHub网站上线了，它为开源项目免费提供Git存储，无数开源项目开始迁移至GitHub，包括jQuery，PHP，Ruby等等。

## 第二章 Git安装和使用 {#第二章-git安装和使用}

### 2.1 Git的安装 {#21-git的安装}

现在三大主流的操作系统，Linux，OS X，Windows，已经全部支持Git

##### Linux {#linux}

（1）Debian或Ubuntu Linux  
直接运行命令 sudo apt-get install git  
（2）其他Linux系统

```
- 从git官网下载源码，解压  
- 依稀输入./config，make，sudo make install 命令

```

##### OS X {#os-x}

从APP Store里面下载xcode（开源，开发Mac和ios APP的必须），xcode集成Git，不过没有默认安装，所以必须我们手动安装，选择菜单“Xcode”-&gt;“Preferences”，在弹出窗口中找到“Downloads”，选择“Command Line Tools”，点“Install”就可以完成安装了。

##### Windows {#windows}

从[https://git-for-windows.github.io下载（网速慢的同学请移步国内镜像\[https://pan.baidu.com/s/1kU5OCOB\#list/path=%2Fpub%2Fgit\]），然后按默认选项安装即可。](https://git-for-windows.github.io%E4%B8%8B%E8%BD%BD%EF%BC%88%E7%BD%91%E9%80%9F%E6%85%A2%E7%9A%84%E5%90%8C%E5%AD%A6%E8%AF%B7%E7%A7%BB%E6%AD%A5%E5%9B%BD%E5%86%85%E9%95%9C%E5%83%8F[https//pan.baidu.com/s/1kU5OCOB#list/path=%2Fpub%2Fgit]），然后按默认选项安装即可。)

因为Git是分布式管理系统，所以要给git设置自己的用户名和邮箱。

```
$ git config --global user.name "Your Name"
$ git config --global user.email "email@example.com"

```

--global 参数是将这个用户名和密码设置为全局。当然你也可以为某一个仓库设置单独的用户名邮箱。

### 2.2 Git的使用 {#22-git的使用}

#### 2.2.1创建版本库 {#221创建版本库}

什么是版本库呢？版本库又名仓库，英文名repository，你可以简单理解成一个目录，这个目录里面的所有文件都可以被Git管理起来，每个文件的修改、删除，Git都能跟踪，以便任何时刻都可以追踪历史，或者在将来某个时刻可以“还原”。

###### 2.2.1.1 git初始化 {#2211-git初始化}

* 新建文件夹
* git init（为了保证不出现奇奇怪怪的问题，最好路径中不要出现中文） 初始化之后，会生成一个隐藏的.git目录，这个文件是git的隐藏文件，是为了来跟踪管理版本库的。

###### 2.2.1.1 添加文件 {#2211-添加文件}

在这之前还要说明一下，其实所有的版本控制工具都只能跟踪文本文件。  
git初始化完成后就可以来跟踪文件的修改与删除了。在这之前，我们来讲一下git的机制

![](https://hxgqh.gitbooks.io/haomotraining/content/assets/git/1.png)

* 将修改的文件添加到暂存区 git add index.html
* 将暂存区中的文件提交到本地master分支 git commit -m "注释"
* git status 和git diff查看文件状态

#### 2.2.2回退版本 {#222回退版本}

当我们做项目的时候，往往会遇到这么一种情况，当我们修改了某一个文档，并且提交到了master分支上面，但是我们并不需要这次的提交，想要返回回去，这时候要怎么办呢？

* git log 查看一下提交的历史，如果觉得内容太多，可以加（--pretty=oneline）这条命令
* 找到你想要返回的哪一个commit的md5码
* git reset --hard commit\_id 返回到这一次提交

![](https://hxgqh.gitbooks.io/haomotraining/content/assets/git/3.png)

其实git的每次提交（commit）都会连城一根线。首先，Git必须知道当前版本是哪个版本，在Git中，用HEAD表示当前版本，上一个版本就是HEAD^，上上一个版本就是HEAD^^，当然往上100个版本写100个^比较容易数不过来，所以写成HEAD~100。

所以如果我们要回退到上一版本 那就输入指令（git reset --hard HEAD^）

###### 那这个是个什么原理呢？ {#那这个是个什么原理呢？}

其实git的内部定义了一个HEAD指针，当回退版本的时候，git仅仅是把HEAD指针从当前节点，指向你回到的那个节点

![](https://hxgqh.gitbooks.io/haomotraining/content/assets/git/4.png)

现在我们可以回退到历史的某个版本了，但是突然间，我们又想要我们会退前的版本，我们只要知道会退钱版本的commit id号就可以了，这时候我们git log一下，会发现现在版本之前的提交信息都没有了！那怎么办呢？其实还是有办法的

* git reflog 查看历史命令，

这样我们就可以找到我们提交会退前版本的id号了，来git reser --hard id 一下就回去啦

#### 2.2.3撤销修改 {#223撤销修改}

有这么一种场景，当我们在这个文件中进行修改，杂七杂八写了一堆，这个时候我觉得还是原来没修改的号，那这个时候我们怎么进行撤销本次操作呢。

* git checkout -- filename

还有一种场景，是我们修改这个文件，修改完成后，已经add到暂存区，这个时候

* git checkout -- filename 将暂存区内的文件，恢复到工作区中，这个时候在执行一次，就恢复到原始数据了。

另外 “--”这个是非常重要的，因为如果不加的话就是切换分支了。

如果我们已经把修改放到了暂存区，还有一钟方法也可以进行撤销修改

* git reset HEAD filename

这里面的HEAD表示最新的版本。

* git rm 文件 删除文件

当我们把文件已经提交到版本库，在工作区中，不小心误删了，那也可以用上面的方法来进行撤销修改。

#### 2.2.4远程仓库 {#224远程仓库}

Git是分布式版本控制系统，同一个Git仓库，可以分布到不同的机器上。怎么分布呢？最早，肯定只有一台机器有一个原始版本库，此后，别的机器可以“克隆”这个原始版本库，而且每台机器的版本库其实都是一样的，并没有主次之分。

找一台电脑充当服务器的角色，每天24小时开机，其他每个人都从这个“服务器”仓库克隆一份到自己的电脑上，并且各自把各自的提交推送到服务器仓库里，也从服务器仓库中拉取别人的提交。

完全可以自己搭建一台运行Git的服务器，不过现阶段，为了学Git先搭个服务器绝对是小题大作。好在这个世界上有个叫GitHub的神奇的网站，从名字就可以看出，这个网站就是提供Git仓库托管服务的，所以，只要注册一个GitHub账号，就可以免费获得Git远程仓库。

在继续阅读后续内容前，请自行注册GitHub账号。由于你的本地Git仓库和GitHub仓库之间的传输是通过SSH加密的，所以，这里需要设置你的SSH key：

\(1\)创建SSH Key。在用户主目录下，看看有没有.ssh目录，如果有，再看看这个目录下有没有id\_rsa和id\_rsa.pub这两个文件，如果已经有了，可直接跳到下一步。如果没有，打开Shell（Windows下打开Git Bash），创建SSH Key：

```
$ ssh-keygen -t rsa -C "youremail@example.com"

```

你需要把邮件地址换成你自己的邮件地址，然后一路回车，使用默认值即可，由于这个Key也不是用于军事目的，所以也无需设置密码

完成之后，找到.ssh目录，打开里面的.id\_rsa.pub\(公钥\)，将它复制到github上面，就可以了。

为什么GitHub需要SSH Key呢？因为GitHub需要识别出你推送的提交确实是你推送的，而不是别人冒充的，而Git支持SSH协议，所以，GitHub只要知道了你的公钥，就可以确认只有你自己才能推送。

##### 2.2.4创建远程库 {#224创建远程库}

在github上我们可以来创建一个远程库，首先在github页面上点击“New Project”来创建一个远程空的仓库，这个时候他会出现这个页面

![](https://hxgqh.gitbooks.io/haomotraining/content/assets/git/6.png)

来提示你可以根据他的方法来新建一个仓库来和它关联，或者是将这个和本地的某个已成型的仓库进行关联。

* git remote add origin git@github.com:yeshijiu/newWork.git
* git push -u origin master

![](https://hxgqh.gitbooks.io/haomotraining/content/assets/git/2.png)

##### 2.2.4从远端克隆 {#224从远端克隆}

开始一个项目，最好的方式是在远端开启一个新项目，，然后从远端克隆。

![](https://hxgqh.gitbooks.io/haomotraining/content/assets/git/6.png)

我们选择这一项之后，github会自动生成README.md文件。然后我们进入到项目中，就可以进行clone了

github的克隆支持多种协议：  
（1）git默认的协议git://  
（2）https协议  
这两种协议有什么区别呢？  
使用https除了速度慢以外，还有个最大的麻烦是每次推送都必须输入口令，但是在某些只开放http端口的公司内部就无法使用ssh协议而只能用https

#### 2.2.3 分支 {#223-分支}

分支是什么意思呢，科幻点来讲，就是平行空间的意思。两个分支，就是两个平行空间，他们互不干扰，在某一时刻，你对令各分支进行了合并，那你就拥有了这两个空间中所有的东西了。

分支在我们的实际开发中的作用是什么呢？ 其实就是便于我们进行各模块的同时开发。

git的分支管理相对于其他的管理工具来说，最大的特点就是快！

##### 2.2.3.1 分支的创建 {#2231-分支的创建}

在版本回退里，你已经知道，每次提交，Git都把它们串成一条时间线，这条时间线就是一个分支。截止到目前，只有一条时间线，在Git里，这个分支叫主分支，即master分支。HEAD严格来说不是指向提交，而是指向master，master才是指向提交的，所以，HEAD指向的就是当前分支。

一开始的时候，master分支是一条线，Git用master指向最新的提交，再用HEAD指向master，就能确定当前分支，以及当前分支的提交点：![](https://hxgqh.gitbooks.io/haomotraining/content/assets/git/8.png)

当我们创建新的分支，例如dev时，Git新建了一个指针叫dev，指向master相同的提交，再把HEAD指向dev，就表示当前分支在dev上：![](https://hxgqh.gitbooks.io/haomotraining/content/assets/git/9.png)

你看，Git创建一个分支很快，因为除了增加一个dev指针，改改HEAD的指向，工作区的文件都没有任何变化！

##### 2.2.3.1 修复bug {#2231-修复bug}

* git stash
* git stash pop

##### 2.2.3.1 无合并分支 {#2231-无合并分支}

* git branch -D

##### 2.2.3.1 多人操作 {#2231-多人操作}

多人协作的工作模式通常是这样：

首先，可以试图用git push origin branch-name推送自己的修改；

如果推送失败，则因为远程分支比你的本地更新，需要先用git pull试图合并；

如果合并有冲突，则解决冲突，并在本地提交；

没有冲突或者解决掉冲突后，再用git push origin branch-name推送就能成功！

如果git pull提示“no tracking information”，则说明本地分支和远程分支的链接关系没有创建，用命令git branch --set-upstream branch-name origin/branch-name。

这就是多人协作的工作模式，一旦熟悉了，就非常简单。

#### 2.2.5 标签 {#225-标签}

发布一个版本时，我们通常先在版本库中打一个标签（tag），这样，就唯一确定了打标签时刻的版本。将来无论什么时候，取某个标签的版本，就是把那个打标签的时刻的历史版本取出来。所以，标签也是版本库的一个快照。

为什么要引入标签呢？因为方便！

* git tag v1.0 打标签
* git tag 查看标签
* git checkout
  切换到标签
* git tag v0.9 commitID 给某一版本的commit来打标签（标签顺序是按照字母来的）
* git show
  查看标签的所有信息
* git tag -a
  -m "version 0.1 released" commitID 给标签添加注释
* git tag -d
  删除标签
* git push origin
  将标签push到远端
* git push origin --tags 将所有标签push到远端
* git push origin :refs/tags/
  删除远端分支\(前提是要先删除本地分支\)

#### 2.2.6 忽略特殊文件\(.gitignore\) {#226-忽略特殊文件gitignore}

在实际的项目开发中，有一些文件是我们没必要push到远端的，比如一些依赖库，一些build时后的产物，以及一些我的本地数据密码之类的文件。当我们修改这希尔文件的时候，git status还是会追踪到，所以git提供了.gitignore文件，来忽略掉这些不想被push的文件或文件夹

.gitignore文件不需要我们从头来写，官方有很多的配置文件，供我们参考，我们直接复制，然后再加上我们自己的一些文件或文件夹就好了。

如果你想提交某一个已经被写入到.gitignore文件的文件，可以采用强制提交

* git add -f App.class

#### 2.2.6 配置别名 {#226-配置别名}

* git config --global alias.co checkout
* git config --global alias.ci commit
* git config --global alias.br branch

配置Git的时候，加上--global是针对当前用户起作用的，如果不加，那只针对当前的仓库起作用。  
配置文件放哪了？每个仓库的Git配置文件都放在.git/config文件中。  
而当前用户的Git配置文件放在用户主目录下的一个隐藏文件.gitconfig中，也可以在这里直接修改

#### 2.2.7 使用gitHub来参与开源项目 {#227-使用github来参与开源项目}

我们一直用GitHub作为免费的远程仓库，如果是个人的开源项目，放到GitHub上是完全没有问题的。其实GitHub还是一个开源协作社区，通过GitHub，既可以让别人参与你的开源项目，也可以参与别人的开源项目。

##### 参与别人的项目 {#参与别人的项目}

拿bootstop为例

* 进入bootstorp（
  [https://github.com/twbs/bootstrap）github主页](https://github.com/twbs/bootstrap%EF%BC%89github%E4%B8%BB%E9%A1%B5)
* 点击fork，将其fork到自己的github
* 从自己的github克隆
* 开发新功能/修复bug
* 推送到自己仓库
* 在GitHub上发起一个pull request。当然，对方是否接受你的pull request就不一定了

## 参考文档： {#参考文档：}

廖雪峰官方网站-Git教程：[http://www.liaoxuefeng.com](http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000)

