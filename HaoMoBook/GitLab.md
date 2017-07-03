# GitLab 培训 {#gitlab-培训}

## 第一章 GitLab简介 {#第一章-gitlab简介}

GitLab 是一个用于仓库管理系统的开源项目。使用Git作为代码管理工具，并在此基础上搭建起来的web服务。 可通过Web界面进行访问公开的或者私人项目。它拥有与Github类似的功能，能够浏览源代码，管理缺陷和注释。可以管理团队对仓库的访问，它非常易于浏览提交过的版本并提供一个文件历史库。团队成员可以利用内置的简单聊天程序\(Wall\)进行交流。它还提供一个代码片段收集功能可以轻松实现代码复用。

## 第二章 GitLab下载安装 {#第二章-gitlab下载安装}

下载安装地址：[https://bitnami.com/stack/gitlab/installer](https://bitnami.com/stack/gitlab/installer)点击下载，然后双击安装，一直点下一步即可。

## 第三章 GitLab的配置与使用 {#第三章-gitlab的配置与使用}

### 1、创建新项目 {#1、创建新项目}

##### 1-1.登录gitlab网址成功后，点击右侧导航条上的 “+” 就可以进入创建项目的页面 {#1-1登录gitlab网址成功后，点击右侧导航条上的--就可以进入创建项目的页面}

![](https://hxgqh.gitbooks.io/haomotraining/content/assets/new_project_1.png)

##### 1-2.在创建工程的页面，按照要求填写项目的名称和可见性等信息。 {#1-2在创建工程的页面，按照要求填写项目的名称和可见性等信息。}

Project path：项目的路径，一般可以认为是项目的名称 Import prject from：从哪导入项目，提供Github/Bitbucket等几个选项 Description（项目的描述）：可选项，对项目的简单描述 Visibility Level（项目可见级别）：提供Private（私有的，只有你自己或者组内的成员能访问）/Internal（所有登录的用户）/Public\(公开的，所有人都可以访问\)三种选项。![](https://hxgqh.gitbooks.io/haomotraining/content/assets/20151118145922637.png)

### 2、添加和配置SSH公钥 {#2、添加和配置ssh公钥}

##### 2-1.SSH（Secure Shell）是一种安全协议，在你的电脑与GitLab服务器进行通信时，我们使用SSH密钥（SSH Keys）认证的方式来保证通信安全。 {#2-1ssh（secure-shell）是一种安全协议，在你的电脑与gitlab服务器进行通信时，我们使用ssh密钥（ssh-keys）认证的方式来保证通信安全。}

##### 2-2.创建 SSH密钥，并将密钥中的公钥添加到GitLab，以便我们通过SSH协议来访问Git仓库。 {#2-2创建-ssh密钥，并将密钥中的公钥添加到gitlab，以便我们通过ssh协议来访问git仓库。}

SSH 密钥的创建需要在终端（命令行）环境下进行，我们首先进入命令行环境。通常在OS X和Linux平台下我们使用终端工具（Terminal），在Windows平台中，可以使用Git Bash工具，git客户端安装目录下git-bash.exe文件

###### A：进入SSH目录：cd ~/.ssh {#a：进入ssh目录：cd-ssh}

（1）如果还没有 ~/.ssh 目录，可以手工创建一个\(mkdir ~/.ssh\)，之后再通过cd ~/.ssh进入SSH目录。 （2）可以通过ls -l命令查看SSH目录下的文件，来确认你是否已经生成过SSH密钥；如果SSH目录为空，我们开始第二步B，生成 SSH 密钥；如果存在id\_rsa.pub这个文件，说明你之前生成过SSH密钥，如何添加多个sshkey也不难，一般很少用，这里不介绍了。

###### B：生成SSH密钥 {#b：生成ssh密钥}

我们通过下面的命令生成密钥，请将命令中的YOUR\_EMAIL@YOUREMAIL.COM替换为你注册gitlab时用的Email地址。 ssh-keygen -t rsa -C "YOUR\_EMAIL@YOUREMAIL.COM" 在SSH生成过程中会出现以下信息，按屏幕的提示操作即可![](https://hxgqh.gitbooks.io/haomotraining/content/assets/20151118182316887.png)

### 3、获取SSH公钥信息 {#3、获取ssh公钥信息}

SSH密钥生成结束后，根据提示信息找到SSH目录，会看到私钥id\_rsa和公钥id\_rsa.pub这两个文件，不要把私钥文件id\_rsa的信息透露给任何人。我们可以通过cat命令或文本编辑器来查看id\_rsa.pub公钥信息。 （1）通过编辑器。使用你熟悉的文本编辑器，比如 记事本、Sublime Text等软件打开id\_rsa.pub，复制里面的所有内容以备下一步使用。

（2）通过cat命令。在命令行中敲入cat id\_rsa.pub，回车执行后命令行界面中会显示id\_rsa.pub文件里的内容，复制后在下一步使用。

（3）通过直接使用命令将id\_rsa.pub文件里的内容复制到剪切板中

Windows: clip &lt; ~/.ssh/id\_rsa.pub

Mac: pbcopy &lt; ~/.ssh/id\_rsa.pub

GNU/Linux \(requires xclip\): xclip -sel clip &lt; ~/.ssh/id\_rsa.pub

### 4、添加SSH公钥到gitlab {#4、添加ssh公钥到gitlab}

##### 4-1.打开gitlab的Profile配置页面，选择SSH Keys,如图： {#4-1打开gitlab的profile配置页面，选择ssh-keys如图：}

![](https://hxgqh.gitbooks.io/haomotraining/content/assets/20151118183709635.png)

##### 4-2.添加SSH公钥。填写Title和Key，其中Title是Key的描述信息，Key是上面复制的SSH公钥的内容，直接粘贴到输入框中保存即可。 {#4-2添加ssh公钥。填写title和key，其中title是key的描述信息，key是上面复制的ssh公钥的内容，直接粘贴到输入框中保存即可。}

![](https://hxgqh.gitbooks.io/haomotraining/content/assets/20151118164823655.png)

### 5、导入项目 {#5、导入项目}

##### 5-1.设置下git的用户名和邮箱 {#5-1设置下git的用户名和邮箱}

在提交代码前，还需要设置下git的用户名和邮箱（最好用英文，不要出现中文），这样提交记录才会在gitlab上显示带有你名字的记录。 在命令行窗口输入（windows需要安装打开Git Bash工具才行）： git config --global user.name"your\_name"

##### 5-2.导新项目到gitlab上 {#5-2导新项目到gitlab上}

如果项目存在，需要导入到gitlab，可以通过命令行直接将项目导入上去。 cd "本地存在项目的路径" git init git remote add origingit@gitlab.com:USERNAME/PROJECTNAME.git git add . git commit -m 'first git demo' git push -u origin master （注：将USERNAME和PROJECTNAME替换成用户名和项目的名称）

##### 5-3.导入项目到本地 {#5-3导入项目到本地}

git clone"你的项目地址"![](https://hxgqh.gitbooks.io/haomotraining/content/assets/20151118183329673.png)

##### 5-4.如何在gitlab上找到你的项目地址位置，请看下图： {#5-4如何在gitlab上找到你的项目地址位置，请看下图：}

![](https://hxgqh.gitbooks.io/haomotraining/content/assets/20151118182853095.png)![](https://hxgqh.gitbooks.io/haomotraining/content/assets/20151123160951678.png)

