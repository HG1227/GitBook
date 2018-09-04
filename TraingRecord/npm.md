### 课堂笔记

Scripts:脚本

Buildbabelindex.js--out-filecompiled.js--scource-mapsmap索引文件压缩以后的路径

Depencies项目依赖项npminstaill--savelodash保存配置信息到package.json里

Devdependencies开发依赖项npminstaill--save-devgulp

cp复制文件

es6转es5工具babelindex.js--out-filecompiled.js--source-map

Es6箭头函数let

# NPM培训 {#npm培训}

## 第一章 NPM介绍 {#第一章-npm介绍}

### 1.1 npm历史 {#11-npm历史}

2009年，[npm（Node 包管理器）初次发布早期预览版；](https://groups.google.com/forum/?hl=en#!topic/nodejs/erDWyS4xPw8)

2011年，[npm 1.0：发布；](https://nodejs.org/en/blog/npm/npm-1-0-released/)

2015年，[npm 支持私有模块](https://www.npmjs.com/private-modules)

npm的出现使我们分享代码或者复用代码变得更加简单。

### 1.2 相关工具 {#12-相关工具}

**bower:**Bower是一个客户端技术的软件包管理器，它可用于搜索、安装和卸载如JavaScript、HTML、CSS之类的网络资源

**yarn:**facebook公司推出的一款快速、可靠、安全的依赖管理工具

### 1.3 未来展望 {#13-未来展望}

npm作为随同nodeJS一起安装的包管理工具，在node包管理领域具有天然的优势，是目前javascript工作者使用最广的js包管理工具；

2016年10月，facebook公司推出一款新的包管理工具yarn，相对于npm具有更快，更可靠，更安全的优势，对npm使用率带来巨大的冲击，但是目前yarn还有一些不完善的地方，比如不能够独立升级某个依赖等，所以在一定时间内npm仍将是使用最广的JavaScript包管理器。

## 第二章 npm安装和使用 {#第二章-npm安装和使用}

### 2.1 npm的安装 {#21-npm的安装}

由于新版的nodejs已经集成了npm，安装nodeJS就安装好npm。

[下载安装 nodeJS 和 npm](https://nodejs.org/en/)

可通过**"npm -v"**来测试是否成功安装。命令如下：

`$ npm -v (可查看npm的安装版本)`

如果安装成功显示：

![](https://hxgqh.gitbooks.io/haomotraining/content/assets/npmversion.png)

安装npm成功之后： a.确认自己的node.js安装的目录：D:\app\node.js。 全局模块安装默认放在C:\Users\Administrator\AppData\Roaming\npm\node\_modules里面。

b.然后，我自己配置了模块安装： node -v npm -v npm config set prefix “D:\app\node.js\node\_global” npm config set cache “D:\app\node.js\node\_cache”

去配置环境变量，

①在系统变量里新建 NODE\_PATH ,值为D:\app\node.js\node\_global， ②在用户变量上的path变量添加 D:\Program Files\nodejs\node\_global。 ③重启下电脑，之后再全局安装了bower：npm i -g bower，之后再查看bower -v就可以显示版本号了，说明安装成功。

npm install bower -g bower init

### 2.2 npm的使用 {#22-npm的使用}

npm 的包安装分为本地安装（local）、全局安装（global）两种，从敲的命令行来看，差别只是有没有-g而已，如下：

```
npm   install  
<
package-name
>
             #本地安装

npm   install -g 
<
package-name
>
       #全局安装
```

下图是在全局环境下安装webpack实例：

![](https://hxgqh.gitbooks.io/haomotraining/content/assets/npminstallwebpack.png)

在项目工程文件下安装依赖包并保存需要使用先创建package.json文件，下面的代码和图片表示在 ~/DeskTop/webDemo 文件中创建 package.json：

```
cd ~/DeskTop/webDemo
npm -init
```

![](https://hxgqh.gitbooks.io/haomotraining/content/assets/npminit.png)

输入npm init 后，根据指示直接按下enter键，即可生成package.json，package.json文件内容如下:

```
{
  "name": "npm",
  "version": "1.0.0",
  "description": "npm",
  "main": "npm",
  "scripts": {
    "test": "echo \"Error: no test specified\" 
&
&
 exit 1"
  },
  "keywords": [
    "npm"
  ],
  "author": "shd",
  "license": "MIT"
}
```

install命令可以使用不同参数，指定所安装的模块属于哪一种性质的依赖关系，即出现在packages.json文件的哪一项中。

* –-save：模块名将被添加到dependencies，可以简化为参数-S。
* –-save-dev: 模块名将被添加到devDependencies，可以简化为参数-D。

```
npm i lodash --save  # --save用于将安装包名称添加到package.json中
```

![](https://hxgqh.gitbooks.io/haomotraining/content/assets/npminstalllodash.png)

![](https://hxgqh.gitbooks.io/haomotraining/content/assets/packagelodash.png)

安装完毕后会在工作目录下产生一个node\_modules目录，其目录下就是安装的各个node模块;

参数使用 --save 表示将在项目文件下将在package.json的项目依赖选项中添加了下载的node模块； 在其他地方使用该项目时，使用npm install即可自动下载在package.json选项中存在的依赖包，而不需要输入module name

更新本地/全局包

```
npm update 
<
package-name
>


npm update -g 
<
package-name
>
```

安装特定版本号的包：

```
npm install 
<
package-name
>
@
<
version
>
```

实例如下图：

![](https://hxgqh.gitbooks.io/haomotraining/content/assets/sureversion.png)

nodejs集成了npm，因此无法全局升级npm，需要在nodejs的安装目录下局部升级npm。例：

`cd "e:\nodejs" 进入node.js的安装目录`

`npm update npm 更新NPM`

### 2.5 package.json详解 {#25-packagejson详解}

* 概述

一般前端项目的根目录下都有个一package.json文件；定义了这个项目所需要的各种模块，以及项目的配置信息（比如名称、版本、许可证等元数据）。 clone项目后，运行`npm install`指令会自动下载该文件里定义的依赖\(包括运行和开发环境下的依赖\)并安装到项目根目录下的`node\_modules`目录下；

package.json文件内部就是一个JSON对象，该对象的每一个成员就是当前项目的一项设置。比如name就是项目名称，version是版本（遵守“大版本.次要版本.小版本”的格式）。

* 主要字段描述

  下图为一个完整的package.json文件的示例图：![](https://hxgqh.gitbooks.io/haomotraining/content/assets/npmpakage.png);

  1. 创建package.json

     创建package.json有两种方法：手动创建和使用命令行：

     ```
     npm init
     ```

     命令行要求回答一些选项；之后再当前目录下生成package.json文件； 在所有问题中只有`name`字段是必填的，其他的都是选填的

  2. script 字段

  scripts指定了运行脚本命令的npm命令行缩写

  图中的指令制定了使用npm run start， npm run build等将要执行的命令；

  1. dependencies、devDependencies字段

  dependencies指明了项目运行的依赖，devDependencies指明了项目开发所依赖的模块；

  他们的值为一个对象，对象的键为项目依赖的模块名，值为模块对应的版本号；表明项目依赖的模块和相应的版本号范围；

  > 指定版本：比如1.2.2，遵循“大版本.次要版本.小版本”的格式规定，安装时只安装指定版本。 波浪号（tilde）+指定版本：比如~1.2.2，表示安装1.2.x的最新版本（不低于1.2.2），但是不安装1.3.x，也就是说安装时不改变大版本号和次要版本号。 插入号（caret）+指定版本：比如ˆ1.2.2，表示安装1.x.x的最新版本（不低于1.2.2），但是不安装2.x.x，也就是说安装时不改变大版本号。需要注意的是，如果大版本号为0，则插入号的行为与波浪号相同，这是因为此时处于开发阶段，即使是次要版本号变动，也可能带来程序的不兼容。 latest：安装最新版本。

  项目中存在package.json文件使用：

  ```
  npm install
  ```

  即可下载安装package.json中定义的模块，并且保存在node\_modules目录下

  如果在项目中添加模块，可以使用在命令行使用相应的参数`--save|-S`和`--save-dev | -D`来将下载的模块信息保存到package.json中

  ```
  npm install --save lodash #将下载的模块信息保存到dependencies对象中；
  npm install --save-dev gulp #将下载的模块信息保存到devDependencies对象中；
  ```

  1. 其他字段

  2. name：项目名，npm install依赖此名称！ 注意： （1）name中不能包含汉子、空格、不能以点号或下划线开头； （2）不要在name中包含js, node字样； （3）这个名字可能在require\(\)方法中被调用，所以应该尽可能短；

  3. version：项目版本 注意：npm采用”语义版本“管理软件包。所谓语义版本，就是指版本号为a.b.c的形式，其中a是大版本号，b是小版本号，c是补丁号。
  4. description：可选字段，必须是字符串。npm search的时候会用到
  5. keywords：关键字，npm search会用到
  6. homepage：项目官网的url
  7. bugs：项目的提交问题的url和（或）邮件地址
  8. License：如果是使用一个普遍的license
  9. Author, contributors：author是一个人，contributors是一组人
  10. engines：指定工作的node的版本
  11. Main: 可选字段。这个字段的值是你程序主入口
      **模块的ID**
      。如果其他用户需要你的包，当用户调用require\(\)方法时，返回的就是这个模块的导出（
      **exports**
      ）
  12. Bin: 可选字段。很多的包都会有执行文件需要安装到PATH中去。这个字段对应的是一个Map，每个元素对应一个{ 命令名：文件名 }。 \`\`\` { "bin" : { "npm" : "./cli.js" } }

  \`\`\`

### 2.3 使用淘宝 NPM 镜像 {#23-使用淘宝-npm-镜像}

* 说明

在国内直接使用 npm 的官方镜像是非常慢的，推荐使用淘宝 NPM 镜像。

淘宝 NPM 镜像是一个完整 npmjs.org 镜像，你可以用此代替官方版本\(只读\)，同步频率目前为 10分钟 一次以保证尽量与官方服务同步。

你可以使用淘宝定制的 cnpm \(gzip 压缩支持\) 命令行工具代替默认的 npm：

* 安装

`$ npm install -g cnpm --registry=https://registry.npm.taobao.org`

* 注意

安装完后最好查看其版本号cnpm -v或关闭命令提示符重新打开，安装完直接使用有可能会出现错误

* tips

> cnpm跟npm用法完全一致，只是在执行命令时将npm改为cnpm。

### 2.4 其他命令 {#24-其他命令}

```
$ npm uninstall express #卸载模块
$ npm update express    #更新模块
$ npm search express    #搜索模块
$ npm info express      #查看模块信息
$ npm ls                #查看已经安装的模块列表
```

### 2.6 理解npm的缓存机制 {#26-理解npm的缓存机制}

`npm install <package>`和`npm update <package>`可以下载和跟新本地的模块；

其中安装之前，npm install会先检查，node\_modules目录之中是否已经存在指定模块；如果存在，就不再重新安装了，即使远程仓库已经有了一个新版本，也是如此。 如果你希望，一个模块不管是否安装过，npm 都要强制重新安装，可以使用-f或–force参数。

它会先到远程仓库查询最新版本，然后查询本地版本。如果本地版本不存在，或者远程版本较新，就会安装。

npm update命令怎么知道每个模块的最新版本呢？

其实，npm 模块仓库提供了一个查询服务，叫做 registry 。以 npmjs.org 为例，它的查询服务网址是[https://registry.npmjs.org/](https://registry.npmjs.org/)。 这个网址后面跟上模块名，就会得到一个 JSON 对象，里面是该模块所有版本的信息。比如，访问[https://registry.npmjs.org/react，就会看到](https://registry.npmjs.org/react%EF%BC%8C%E5%B0%B1%E4%BC%9A%E7%9C%8B%E5%88%B0)react 模块所有版本的信息。 它跟下面命令的效果是一样的。

```
$ npm view react
$ npm info react
$ npm show react
$ npm v react
```

npm install或npm update命令，从 registry 下载压缩包之后，都存放在本地的缓存目录。 这个缓存目录，在 Linux 或 Mac 默认是用户主目录下的.npm目录，在 Windows 默认是%AppData%/npm-cache。通过配置命令，可以查看这个目录的具体位置。

```
$ npm config get cache
$HOME/.npm
```

浏览该文件：

```
$ ls ~/.npm 
$ npm cache ls
```

你会看到里面存放着大量的模块，储存结构是{cache}/{name}/{version};

每个模块的每个版本，都有一个自己的子目录，里面是代码的压缩包package.tgz文件，以及一个描述文件package/package.json。 除此之外，还会生成一个{cache}/{hostname}/{path}/.cache.json文件。比如，从 npm 官方仓库下载 react 模块的时候，就会生成registry.npmjs.org/react/.cache.json文件。 这个文件保存的是，所有版本的信息，以及该模块最近修改的时间和最新一次请求时服务器返回的 ETag 。

对于一些不是很关键的操作（比如npm search或npm view），npm会先查看.cache.json里面的模块最近更新时间，跟当前时间的差距，是不是在可接受的范围之内。如果是的，就不再向远程仓库发出请求，而是直接返回.cache.json的数据。 .npm目录保存着大量文件，清空它的命令如下。

```
$ rm -rf ~/.npm/*
# 或者
$ npm cache clean
```

### 2.7 模块的安装过程 {#27-模块的安装过程}

* 发出npm install命令
* npm 向 registry 查询模块压缩包的网址
* 下载压缩包，存放在~/.npm目录
* 解压压缩包到当前项目的node\_modules目录

注意，一个模块安装以后，本地其实保存了两份。一份是~/.npm目录下的压缩包，另一份是node\_modules目录下解压后的代码。

## 参考文档： {#参考文档：}

NPM使用介绍-菜鸟教程：[http://www.runoob.com/nodejs/nodejs-npm.html](http://www.runoob.com/nodejs/nodejs-npm.html)

Node.js&NPM的安装与配置：[http://www.infoq.com/cn/articles/nodejs-npm-install-config](http://www.infoq.com/cn/articles/nodejs-npm-install-config)

node.js的配置以及向git提交代码：[http://www.tuicool.com/articles/aiaQR3b](http://www.tuicool.com/articles/aiaQR3b)

知乎上关于node.js 的话题：[https://www.zhihu.com/topic/19569535/top-answers](https://www.zhihu.com/topic/19569535/top-answers)

知乎中关于npm的话题：[https://www.zhihu.com/question/24414899](https://www.zhihu.com/question/24414899)

npm，bower，jamjs等包管理工具各自的特性及区别：[https://www.zhihu.com/question/24414899](https://www.zhihu.com/question/24414899)

package.json中文文档：[http://www.mujiang.info/translation/npmjs/files/package.json.html](http://www.mujiang.info/translation/npmjs/files/package.json.html)

