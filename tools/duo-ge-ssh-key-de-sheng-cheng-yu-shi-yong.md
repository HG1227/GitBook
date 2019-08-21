## 生成多个ssh\_key的方法

### 首先输入用户名以及邮箱地址

`git config --global user.name "Your Name"`  
`git config --global user.email "Your Email Address"`

### 生成第一个ssh

`ssh-keygen -t rsa -C "Your Email Address"`  
Ps.`ssh-keygen -t rsa -C "13683265113@163.com"`

### 生成第二个ssh

#### 方法一:需要在指令后加 -f 'Your Name' 加以区分

`ssh-keygen -t rsa -C “Your Email Address” -f 'Your Name'`  
Ps.`ssh-keygen -t rsa -C “gaotianyang@haomo-studio.com” -f 'gaotianyangHM'`  
`(此时会在.ssh下生成gaotianyangHM & gaotianyangHM.pub)`

#### 方法二:需要在指令执行后 在存储时起名字

`ssh-keygen -t rsa -C "Your Email Address"`  
`Enter file in which to save the key (/c/Users/Lenovo/.ssh/id_rsa):'Your Name'`  
Ps.`Enter file in which to save the key (/c/Users/Lenovo/.ssh/id_rsa):'gaotianyangHM'`  
`(此时同样会在.ssh下生成gaotianyangHM & gaotianyangHM.pub)`![](https://camo.githubusercontent.com/6f5d33c75b337d2d17600d2e13b68d91ec7d308e/687474703a2f2f696d672e626c6f672e6373646e2e6e65742f32303135303131323135333735373335333f77617465726d61726b2f322f746578742f6148523063446f764c324a736232637559334e6b626935755a5851766158527465576876625755784f546b772f666f6e742f3561364c354c32542f666f6e7473697a652f3430302f66696c6c2f49304a42516b46434d413d3d2f646973736f6c76652f37302f677261766974792f536f75746845617374 "ssh生成图例")

## 多个ssh\_key的使用

### 在.ssh/下创建config文件 内容如下

`Host github.com`  
`HostName github.com`  
`PreferredAuthentications publickey`  
`IdentityFile ~/.ssh/id_rsa`

`Host my.github.com`  
`HostName github.com`  
`PreferredAuthentications publickey`  
`IdentityFile ~/.ssh/my`

Ps.`Host名字随意，接下来会用到`

### 测试配置是否正确

`ssh -T git@github.com`

![](https://camo.githubusercontent.com/9b34d5aa1297cc053a35dcb425cbf12fb45b2fc7/687474703a2f2f696d672e626c6f672e6373646e2e6e65742f3230313530313132313534323038303932 "测试图例1")  
`ssh -T git@gaotianyangHM.github.com`![](https://camo.githubusercontent.com/9e843e8820a365a1a25cb4179a96c4f112d57413/687474703a2f2f696d672e626c6f672e6373646e2e6e65742f3230313530313132313534323137303632 "测试图例2")  
Ps.`如果出现Hi xxx!You've successfully authenticated 就说明连接成功了`

测试结果失败，未成功添加处理办法：

* 刷新新添加的ssh

`ssh-add -l`

[添加ssh讲解链接](http://debugtalk.com/post/head-first-git-authority-verification/)

* 重启电脑\(待测试\)

### 现在就以下种情况给出不同的做法：

#### 1、本地已经创建或已经clone到本地：

##### 如下两种解决方法：

打开.Git/config文件  
`#更改[remote "origin"]项中的url中的`  
`#my.github.com 对应上面配置的host`  
`[remote "origin"]`  
`url = git@my.github.com:itmyline/blog.git`  
或者在Git Bash中提交的时候修改remote  
`$ git remote rm origin`  
`$ git remote add origin git@my.github.com:itmyline/blog.git`

#### 2、clone仓库时对应配置host对应的账户

`#my.github.com对应一个账号`  
`git clone git@my.github.com:username/repo.git`  
Ps.`git clone git@HM.github.com:username/repo.git`  
Ps.`git clone git@gtyHM.github.com:username/repo.git`

### 借鉴文章链接

#### [生成多个key](http://blog.csdn.net/u012365926/article/details/52293036)

#### [多个key之间切换](http://blog.csdn.net/itmyhome1990/article/details/42643233)



