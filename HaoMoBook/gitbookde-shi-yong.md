## gitbook安装

node的安装 查看node的版本号 在终端输入

```
node -v
```

查看npm的版本号 在终端输入

```
npm -v
```

如果以上步骤没有出错，接下来就可以安装gitbook了

```
npm install gitbook -g
npm install gitbook-cli -g
```

## 初始化项目

```
gitbook init
```

会发现目录下面多了2个文件，\*\*README.md\*\*和\*\*SUMMARY.md\*\*

README.md 和 SUMMARY.md 是两个必须文件

README.md 是对书籍的简单介绍

SUMMARY.md 是书籍的目录结构

* SUMMARY.md目录

![](/assets/GitBookUse1.png)

SUMMARY.md 是书籍的目录结构，格式如上，每一行对应一个相应的文件

* gitbook init

![](/assets/GitBookUse2.png)

执行 gitbook init 会根据 SUMMARY.md 目录生成对应的文件夹和 md 文件，每一个 md 文件对应每一章节，每一章节的内容在对应的 md 文件里编辑。

如果想要新增章节，可以在 SUMMARY.md 里面新增，然后执行 gitbook init 就会新增对应的 md 文件，原有文件不会变化；如果想要删除章节，在 SUMMARY.md 里面删除，然后执行 gitbook init 想要删除的 md 文件并不会删除，需要手动删除。

* gitbook build

![](/assets/GitBookUse3.png)

gitbook build . ./output

//output为要输出的目录，不写默认为\_book目录

执行 gitbook build 会根据 gitbook init 生成的 md 文件生成对应的 html 文件

* gitbook serve

本地预览，[http://localhost:4000](http://localhost:4000)

* 其他配置

新建book.json，可以做一些配置，比如标题，作者，指定readme文件，关闭分享链接等。

![](/assets/GitBookUse4.png)

[http://blog.csdn.net/axi295309066/article/details/61420694](http://blog.csdn.net/axi295309066/article/details/61420694)

类似于github的wiki？开源公开？

Gitbook简介

基于node.js的命令行工具语法为markdown

Npminstallgutbook-cli-g

是什么干什么

用于项目中各类内容的功能\(说明文档\)

summary目录会直接创建目录中的内容

Gitbookbuild创建html

Gitbookserve\(window环境可能有问题\)

如何分享?

放置于gitbook上可以类似于github的功能多人共同维护同一本书

说明文档

检测代码规范工具es-Lint

怎么用

Gitbook-cli

语法--markdown

Webstorm安装markdown插件

\#一级标题

\#\#二级标题

\#\#\#三级标题

···

代码块

···

&gt;标注块

-无序列表

-无序列表

1.有序列表

2.有序列表

public书写的gitbook

