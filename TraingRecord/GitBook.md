# GitBook

#### 作者：高天阳
#### 邮箱：13683265113@163.com

```
更改历史

* 2019-07-24	    高天阳	gitbook使用代码高亮插件
* 2018-09-14	    高天阳	gitbook生成PDF
* 2018-01-07	    高天阳	gitbook serve报错处理方法
* 2017-11-12	    高天阳	增加类比内容，更改页面格式
* 2017-07-15	    高天阳	更改内容
* 2017-06-01        江伟	    初始化文档

```

## 历史、现状和发展

### [历史](https://www.gitbook.com/about)

GitBook创建于2014年中期，致力于为文档，数字书写和出版创建一个现代化的简单解决方案。

我们已经开始构建一个[开源](https://github.com/GitbookIO/gitbook)的格式。哲学是简单到优雅的地步，消除内容创作者的分心和关注，使他们可以自由地写作。
从那时起，我们已经长大了帮助超过**25万人**一起工作到写作**150,000册图书**投放到**20M**的游客每月。

### 简介

GitBook 是一个基于 Node.js 的命令行工具，可使用 Github/Git 和 Markdown 来制作精美的电子书。

GitBook可以把你的书本生成为静态网站以及PDF、ePub\(苹果和google的设备支持这种格式\)、Mobi\(kindle支持的格式\)格式的电子书。

- 个人观点:这类应该是未来书籍出版的方向

### 特点 

- **更新简单**，使用[Git](https://baike.baidu.com/item/GIT/12647237)(分布式版本控制系统)或者web编辑器发布和更新你的电子书是很容易的；
- **版本管理**，Gitbook是以GIT-scm为基础的.一句简单的`git push`代码就可以发布一个新版本；
- **Markdown**，电子书是使用的[Markdown](http://www.jianshu.com/p/63dc1bc6b1d9)或者[AsciiDoc](http://ju.outofmemory.cn/entry/95397)语法，全面支持[TeX](https://baike.baidu.com/item/TeX/3794463?fr=aladdin)/[Math](https://baike.baidu.com/item/Math/10588698?fr=aladdin)方程式；
- **Github**，通过Gitbook可以在Gihub上同步更新你的电子书；
- **数据分析**，记录PV和下载，提供强大的`洞察力？`；
- **编辑**，使用web编辑器编辑你的内容，更新之前可以预览内容；
- **个性化品牌**，个人主页和自定义域名；
- **合作**，结构化你的流程，安全的访问控制

## 安装和使用

### 安装

#### 安装GitBook

[gitbook](https://github.com/GitbookIO/gitbook)的安装非常简单，详细指南可以参考
[gitbook 文档](https://github.com/GitbookIO/gitbook)。

这里的安装只需要一步就能完成！

```
$ npm install gitbook -g
```

需要注意的是：用户首先需要安装 nodejs，以便能够使用 npm 来安装 gitbook。

#### 安装GitBook脚手架

##### windows下安装GitBook脚手架

输入命令，全局安装gitbook。

```
$ npm install gitbook-cli -g
```

![](../../assets/gitbook/gitbook-cliInstall.jpeg)

![](../../assets/gitbook/gitbook-cliInstall2.jpeg)

在CMD窗口中输入

mkdir   mybook       创建文件夹

切换到目录下.

![](../../assets/gitbook/mkdirGitBook.png)

切换文件夹后在当前文件目录下的在窗口中输入如下命令

##### Mac下安装GitBook脚手架

GitBook 是一个基于 Node.js 的命令行工具；安装gitbook-cli需要首先安装nodeJS,安装gitbook-cli:

```
npm install gitbook-cli -g   #安装gitbook-cli

gitbook --version            #检测是否安装成功
```

![](../../assets/gitbook/gitbookversion.png)

### 使用

- 配置
    - title
    - author
    - description
    - language
    - links
    - styles
    - plugins
    - pluginsConfig
- gitbook插件
    - Disqus
    - Search Pro
    - Advanced Emoji
    - Github
    - Ace Plugin
    - Emphasize
    - KaTex
    - Include Codeblock
    - Splitter
    - Mermaid
    - Sharing
    - Tbfed-pagefooter
    - Toggle Chapters
    - Sectionx
    - Codeblock-filename
    - ga
    - baidu
- gitbook输出方式
    - 静态站点：GitBook默认输出该种格式
    - PDF：需要安装gitbook-pdf依赖
    - eBook：需要安装ebook-convert
- gitbook插件

### 示例

### GitBook章节和子章节

在学习使用之前，我们首先需要了解一下`SUMMARY.md`是干什么的。GitBook使用文件 `SUMMARY.md` 来定义书本的章节和子章节的结构。
文件 `SUMMARY.md` 被用来生成书本内容的预览表。

`SUMMARY.md` 的格式是一个简单的链接列表，链接的名字是章节的名字，链接的指向是章节文件的路径。

子章节被简单的定义为一个内嵌于父章节的列表。

简单实例:

```
# 概要

* [卷 I](part1/README.md)
    * [写作很棒](part1/writing.md)
    * [GitBook很酷](part1/gitbook.md)
* [卷 II](part2/README.md)
    * [期待反馈](part2/feedback_please.md)
    * [更好的写作工具](part2/better_tools.md)
```

gitbook 的基本用法非常简单，基本上就只有两步：

1. 使用`gitbook init`初始化书籍目录
2. 使用`gitbook serve`预览书籍
2. 使用`gitbook build`编译书籍

下面将结合一个非常简单的实例，来介绍 gitbook 的基本用法。

#### GitBook初始化

首先，创建如下目录结构：

```
$ tree book/
book/
├── README.md
└── SUMMARY.md

0 directories, 
2 files
```

README.md 和 SUMMARY.md 是两个必须文件

* README.md 文件内容作为创建的gitbook的简介；
* SUMMARY.md 文件内容为创建的gitbook的目录信息；

![](../../assets/gitbook/readme.png)  
![](../../assets/gitbook/summary.png)

再次使用`gitbook init`初始化文件夹如图：  
![](../../assets/gitbook/gitbookinitfile.png)

这样我们就会在自己的电脑上创建对好应的md文件；

#### GitBook预览

当你在自己的电脑上编辑好图书之后，你可以使用Gitbook的命令行进行本地预览：

`gitbook serve`;之后，浏览器打开`localhost:4000`;如下图：  
![](../../assets/gitbook/gitbookserve.png)  
![](../../assets/gitbook/gitbookhtml.png)

`git build .`默认生成了\_book文件夹存储生成的html文件,可以使用：

```
git build . build   #生成build文件存储html文件
```

#### 在线协作文档

gitbook可以帮助我们团队在线编写gitbook，协作编辑文档。

**tips:** 首先要有git账号:

[gitbook地址](https://www.gitbook.com/)

[git地址](https://github.com/)

接下来登录gitbook,使用git账号登录：

![](../../assets/gitbook/gitbooklogin.png)

进入主页选择点击create book，进入创建书籍页面，选择创建github类型书籍：

![](../../assets/gitbook/gitbookhub.png)

点击图中2所指按钮，进入github页面；在github上安装gitbook；并创建gitbook相关创库：

![](../../assets/gitbook/githubookinstall.png)  
![](../../assets/gitbook/githubbuild.png)

接下里回到gitbook网站，新建书籍，选择github出现填写title等，选择刚才创建的仓库；然后点击`Create book`按钮，生成新的书籍；

![](../../assets/gitbook/createbook.png)  
![](../../assets/gitbook/bookjiemian.png)

这样我们就可以通过在github上上传我们创建的book，然后显示在gitbook上；

按照github上指示将本地创建的book上传到对应的仓库；

![](../../assets/gitbook/gitpushbook.png)

在gitbook上刷新书籍我们就能看到这本书书籍了；在setting里通过添加成员并设置权限就可以实现多成员共同维护这本书籍了~

![](../../assets/gitbook/showbook.png)  
![](../../assets/gitbook/addmember.png)

### 最佳实践

#### [Linux系统上如何同时部署两个gitbook服务](http://blog.csdn.net/moxiaomomo/article/details/53026645)

gitbook启动的web 服务默认监听4000端口，而重启监控进程默认监听35729端口。一般这样可以启动一个电子书web服务:

```
gitbook serve /somepath/your_docuemtn_dir/  
```

本地就可以这样来访问:  http://localhost:4000 。

如果要启动另一部电子书服务的话， 就需要同时修改web端口和监控进程端口， 类似这样:

```
gitbook serve --lrport 35288 --port 4001 /path2/your_another_doc_dir/  
```

否则会报如下错误:

```
You already have a server listening on 35729  
You should stop it and try again.  
```

或者如下错误:

```
Starting server ...  
  
events.js:72  
        throw er; // Unhandled 'error' event  
              ^  
Error: listen EADDRINUSE  
    at errnoException (net.js:905:11)  
    at Server._listen2 (net.js:1043:14)  
    at listen (net.js:1065:10)  
    at Server.listen (net.js:1139:5)  
    at /root/.gitbook/versions/2.6.7/lib/utils/server.js:81:22  
    at _fulfilled (/root/.gitbook/versions/2.6.7/node_modules/q/q.js:787:54)  
    at self.promiseDispatch.done (/root/.gitbook/versions/2.6.7/node_modules/q/q.js:816:30)  
    at Promise.promise.promiseDispatch (/root/.gitbook/versions/2.6.7/node_modules/q/q.js:749:13)  
    at /root/.gitbook/versions/2.6.7/node_modules/q/q.js:810:14  
    at flush (/root/.gitbook/versions/2.6.7/node_modules/q/q.js:108:17)  
```

最后, 贴上gitbook的官方用法说明:

```
$ gitbook help  
  
  build [book] [output]      build a book  
    --format      Format to build to (Default is website; Values are website, json, ebook)  
    --log      Minimum log level to display (Default is info; Values are debug, info, warn, error, disabled)  
  
  pdf [book] [output]      build a book to pdf  
    --log      Minimum log level to display (Default is info; Values are debug, info, warn, error, disabled)  
  
  epub [book] [output]      build a book to epub  
    --log      Minimum log level to display (Default is info; Values are debug, info, warn, error, disabled)  
  
  mobi [book] [output]      build a book to mobi  
    --log      Minimum log level to display (Default is info; Values are debug, info, warn, error, disabled)  
  
  serve [book]      Build then serve a gitbook from a directory  
    --port      Port for server to listen on (Default is 4000)  
    --lrport      Port for livereload server to listen on (Default is 35729)  
    --watch      Enable/disable file watcher (Default is true)  
    --format      Format to build to (Default is website; Values are website, json, ebook)  
    --log      Minimum log level to display (Default is info; Values are debug, info, warn, error, disabled)  
  
  install [book]      install plugins dependencies  
  
  init [directory]      create files and folders based on contents of SUMMARY.md  
```

#### [提交gitbook代码时报403](http://www.jianshu.com/p/77b0340a02f3)

> 处理方法

查看本机用户名密码获取方式

```
git config --local credential.helper
git config --global credential.helper
git config --system credential.helper
```

此时应显示为`osxkeychain`钥匙串
如果不是需编辑`.gitconfig`文件的`[helper]`

Mac系统打开钥匙串访问，查看到对应gitbook的秘钥(你会发现此秘钥不是你自己的账号密码)，并删除它。

再次提交代码，会提示你输入用户名密码。输入后成功提交。

#### gitbook serve报错

windows系统gitbook serve时报错找不到lunr.min.js

![](../../assets/gitbook/gitbook01.png)

> 处理方法

按下面顺序执行命令

```
$ gitbook init
$ gitbook build
$ gitbook serve
```

#### GitBook生成pdf

安装calibre插件

玩过kindle的都知道，calibre是一款非常方便的开源电子书转换软件。在这里，我们也是用到ebook-convert这个插件。

首先在calibre官网下载插件，[插件下载地址](https://calibre-ebook.com/download)。下载适合自己系统的版本。

下载到电脑之后我做了很多尝试，刚下载之后我兴冲冲的去使用`gitbook pdf .mypdf.pdf`指令，结果发现提示ebook-convert未安装。

这里我通过咨询了一些大神，在这个过程中他们给了我很大的帮助。也查看了很多教程，所有教程中都说了两个问题

将安装的calibre放在系统应用中，然后将app添加到path中。

> 这个说实话我也没怎么看懂，但是下面我会详细的说这一步如何操作。

执行一个命令

```
sudo ln -s /Applications/calibre.app/Contents/MacOS/ebook-convert /usr/local/bin
```

以上两部我都做了，最终也成功的将Gitbook导出了PDF，但具体是哪一步起了作用，我估计是第二步，不过在教程中我优先推荐使用第二步。
第二步遇到的坑是，在网上我们找到的教程只是输入`ln -s /Applications/calibre.app/Contents/MacOS/ebook-convert /usr/local/bin`，
但是执行多次都没有结果，WIN系统执行这步可能已经正确了。因为Mac环境权限的原因，这里加入sudo重新执行即可。

执行完成之后，重新进入书籍目录。

```
huixingdeMacBook-Air:import huixing$ cd jianli
huixingdeMacBook-Air:jianli huixing$ gitbook pdf . jianli.pdf
info: 7 plugins are installed 
info: 6 explicitly listed 
info: loading plugin "highlight"... OK 
info: loading plugin "search"... OK 
info: loading plugin "lunr"... OK 
info: loading plugin "sharing"... OK 
info: loading plugin "fontsettings"... OK 
info: loading plugin "theme-default"... OK 
info: found 1 pages 
info: found 7 asset files 
info: >> generation finished with success in 7.5s ! 
info: >> 1 file(s) generated
```

执行完以上代码，进入书籍目录，即可看到已经转换完成的PDF了。大功告成！

#### GitBook book.json配置

##### title 设置书本的标题

“title” : “私人笔记”

##### author 作者的相关信息

“author” : “gaotianyang”

##### description 本书的简单描述

“description” : “gaotianyang的私人笔记”

##### language Gitbook使用的语言

“language” : “zh-hans”

版本2.6.4中可选的语言如下：

en, ar, bn, cs, de, en, es, fa, fi, fr, he, it, ja, ko, no, pl, pt, ro, ru, sv, uk, vi, zh-hans, zh-tw

##### links 在左侧导航栏添加链接信息

```json
{
    "links": {
        "sidebar": {
            "Personal Book": "http://www.gtwteam.com"
        }
    }
}
```

##### styles 自定义页面样式

```json
{
    "styles": {
        "website": "styles/website.css",
        "ebook": "styles/ebook.css",
        "pdf": "styles/pdf.css",
        "mobi": "styles/mobi.css",
        "epub": "styles/epub.css"
    }
}
```

例如使`h1 h2`标签有下划线， 可以在website.css中设置

```css
h1 , h2{
    border-bottom: 1px solid #EEEEEE;
}
```

##### plugins 插件列表

可以在插件前面加`-`符号删除默认插件，默认五种插件如下

* highlight：代码高亮
* search：导航栏查询功能（不支持中文）
* sharing：右上角分享功能
* font-settings：字体设置（最上方的"A"符号）
* livereload：为GitBook实时重新加载

## 同类技术对比(列表)

### GitBook

- 喜欢:
    - 多人协作及团队支持
    - 基于GIT的版本历史和还原
    - 在线写作/离线写作
    - 关注、分享和收藏功能
    - 文档导入和导出支持
    - 支持发布在github博客系统上，别人可以来fork可以来帮你纠错，给你发pull request。
    - 独立的应用程序。
    - 这是一家书店。
    - 发布到大型商店。
- 不喜欢：
    - 不翻墙的时候打开会比较慢。
    - 丑陋的MSWord-like排版。
    - 根本没有“社交协作”，似乎只是由Git支持。不确定应用程序是否支持小规模协作（双人作者），或者您必须自己处理Git复杂性。
    - 似乎技术导向。没有小说类别。

### kanCloud——专注于文档在线创作、协作、分享和托管

看云的发布版本和编辑版本是分离的，而且看云对技术文档做了一些优化，并且支持 API 文档（包括在线调试）。
最新更新支持插入视频。另外一个在国内定价收费也方便。

- 喜欢:
    - 全新体验的Markdown编辑器，让你的创作更有灵感
    - 响应式设计的阅读方式
    - 数学公式和目录导航
    - 支持插入流程图/时序图
    - 创建私有文档以及文档权限控制
    - 在线写作/离线写作
    - 基于GIT的版本历史和还原
    - 多人协作及团队支持
    - 文档更新动态和评论通知
    - 关注、分享和收藏功能
    - 文档导入和导出支持
    - 域名绑定/导航自定义
    - 支持文档统计功能
    - 支持插入优酷视频
    - 文档打赏和付费阅读
    - 离线写作客户端
    - 阅读客户端（支持安卓和IOS）

#### Leanpub——Publish Early, Publish Often

- 喜欢：
    - 精益出版。
    - 作者与读者的互动非常棒。
    - 他们的PDF输出是美丽的。
    - 这是一个书店（90％版税！）与社交网络方面。
    - 创建捆绑包，与其他作者分享版税等非常容易。真的很棒的功能。
    - 营销工具真棒。与Google Analytics（分析）整合
- 不喜欢：
    - 我无法下载他们的工具链（但在“Markdown to Ebook”[0]之后，本地工作流程有点可重现）
    - 不依赖于Git，但在Dropbox中。没有适当的版本控制。
    - 没有合作。
    - 不发布到主要书店（但允许你这样做）。

#### penflip——在线文本编辑工具

Penflip似乎更适合你的想法（注意：现在我知道它为什么适合你的想法），像GitHub一样合作。
- 喜欢：
    - 多人协作及团队支持
- 不喜欢：
    - 与书店没有整合。
    - 这不是一个书店，你不能轻易发现书籍。
    - 看起来更像是一个使用FSF意义上的“免费”的“免费书籍”平台。
    - 很难找到一本完整的书来窥探，但是输出看起来和GitBook一样丑陋。AFAIK他们让你自定义输出，
    但似乎排版不是LaTeX-like，怀疑它不可以胜任。默认是非常重要的，它应该是美丽的开箱即用。

## 参考资料

* [Gitbook使用记录--电子书制作工具](http://www.jianshu.com/p/63dc1bc6b1d9)
* [Gitbook官方文档](https://www.gitbook.com/blog/features)
* [Gitbook实用配置及插件介绍](https://www.cnblogs.com/zhangjk1993/p/5066771.html)
* [Gitbook对比评论](https://news.ycombinator.com/item?id=8215620)
* [Gitbook提交报403](http://www.jianshu.com/p/77b0340a02f3)
* [Mac环境安装Gitbook，并导出PDF教程](https://www.jianshu.com/p/4824d216ad10)
* [gitbook的插件配置](https://www.cnblogs.com/yonguo123/p/9524024.html)
* [gitbook安装与使用](https://blog.csdn.net/fghsfeyhdf/article/details/88403548)
* [gitbook常用插件简介](https://blog.csdn.net/qq_37149933/article/details/64170653)
* [gitbook安装代码高亮插件：Prism](https://www.crifan.com/gitbook_install_code_highlight_plugin_prism/)
* [gitbook菜单序号设置](https://www.crifan.com/gitbook_add_chapter_index_number/)