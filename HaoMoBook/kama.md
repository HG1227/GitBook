### Kama课堂笔记

执行单元测试的管理工具

#### 安装指令

npm init

\(npm install cnpm\)

cnpm install karma --save-dev

karma start\(测试karma是否安装成功\)

karma init\(初始化karma\*\*必须使用Git CMD\*\*\)

cnpm install karma-jasmine karma-chrome-launcher jasmine-core --save-dev\(安装js测试插件、浏览器自启动插件\)

#### 配置文件

basePath:相对配置文件监听的路径\(相对路径\)

Files:需要被监听

Exclude:被忽略监听的

代码覆盖率必须在所有JS没有报错的情况下才能监听

是否必须返回值才能判断不需要

执行单元测试的管理工具

配置文件

basePath:相对配置文件监听的路径\(相对路径\)

Files:需要被监听

Exclude:被忽略监听的

代码覆盖率必须在所有JS没有报错的情况下才能监听

是否必须返回值才能判断不需要

安装和使用Karma-Jasmine进行自动化测试

[安装和使用Karma-Jasmine](http://www.tuicool.com/articles/aemI7b6)

前端自动化测试工具--使用karma进行javascript单元测试

[http://m.blog.csdn.net/article/details?id=52815596](http://m.blog.csdn.net/article/details?id=52815596)

JavaScript 单元测试框架：Jasmine 初探

[https://www.ibm.com/developerworks/cn/web/1404\_changwz\_jasmine/](https://www.ibm.com/developerworks/cn/web/1404_changwz_jasmine/)

Jasmine 部分API说明

[http://m.blog.csdn.net/article/details?id=38562257](http://m.blog.csdn.net/article/details?id=38562257)

jasmine官方api参考

[http://www.cnblogs.com/stephenykk/p/4539200.html](http://www.cnblogs.com/stephenykk/p/4539200.html)

# Karma {#85-karma}

## 第一章：Karma简介 {#第一章：karma简介}

### 1.1简介 {#11简介}

**1.Karma介绍**

Karma是由Google团队开发的一套前端测试运行框架，karma会启动一个web服务器，将js源代码和测试脚本放到PhantomJS或者Chrome上执行。

Karma是Testacular的新名字，在2012年google开源了Testacular，2013年Testacular改名为Karma。Karma是一个让人感到非常神秘的名字，表示佛教中的缘分，因果报应，比Cassandra这种名字更让人猜不透！

Karma是一个基于Node.js的JavaScript测试执行过程管理工具（Test Runner）。该工具可用于测试所有主流Web浏览器，也可集成到CI（Continuous integration）工具，也可和其他代码编辑器一起使用。这个测试工具的一个强大特性就是，它可以监控\(Watch\)文件的变化，然后自行执行，通过console.log显示测试结果。

**2.Jasmine介绍**

Jasmine （茉莉）是一款 JavaScript BDD（行为驱动开发）测试框架，它不依赖于其他任何 JavaScript 组件。它有干净清晰的语法，让您可以很简单的写出测试代码。对基于 JavaScript 的开发来说，它是一款不错的测试框架选择。

### 1.2相关工具 {#12相关工具}

## 第二章Karma的安装使用 {#第二章karma的安装使用}

### 2.1Karma的安装 {#21karma的安装}

**1.创建项目并初始化。**![](https://hxgqh.gitbooks.io/testautomization/content/assets/WechatIMG68.jpeg)**2.安装cnpm（使用npm安装Karma速度慢），安装好cnpm后,使用cnpm安装Karma执行**：

`cnpmm isntall karma --save-dev`

**3.安装karma-jasmine/karma-chrome-launcher/jasmine-core插件**

`cnpm install karma-jasmine karma-chrome-launcher jasmine-core --save-dev`

![](https://hxgqh.gitbooks.io/testautomization/content/assets/WechatIMG70.jpeg)

**4.安装karma-cli**

karma-cli用来简化karma的调用，安装命令如下，其中-g表示全局参数，这样今后可以非常方便的使用karma了：

`cnpm isntall -g karma-cli`

**5.开启Karma**

`karma start`

![](https://hxgqh.gitbooks.io/testautomization/content/assets/WechatIMG71.jpeg)![](https://hxgqh.gitbooks.io/testautomization/content/assets/WechatIMG72.jpeg)

### 2.2Karma+jasmine的配置 {#22karmajasmine的配置}

1**.执行**`karma init`**命令进行karma的配置**

![](https://hxgqh.gitbooks.io/testautomization/content/assets/WechatIMG69.jpeg)

**说明：**

1. 选择测试框架：我们当然选jasmine

2. 是否添加Require.js插件

3. 选择浏览器： 我们选Chrome

4. 测试文件路径设置，文件可以使用通配符匹配，比如\*.js匹配指定目录下所有的js文件（实际操作中发现该路径是karma.conf.js文件的相对路径）

5. 在测试文件路径下，需要排除的文件

6. 是否允许Karma监测文件，yes表示当测试路径下的文件变化时，Karma会自动测试

### 2.3karma使用 {#23karma使用}

1.在项目中创建TestFiles文件夹，在文件夹中分别创建jasmineTest.js和test.js，创建完成后目录结构如下：

![](https://hxgqh.gitbooks.io/testautomization/content/assets/WechatIMG73.jpeg)

_在两个js文件中分别输入：_

test.js内容：

```
function TT() {    
  return "abc";
}

```

jasmineTest.js内容：

```
describe("A suite of basic functions", function() {
    it("test", function() {
        expect("abc").toEqual(TT());
    });
});

```

2.修改karma.conf.js的配置：完整内容如下：

![](https://hxgqh.gitbooks.io/testautomization/content/assets/WechatIMG74.jpeg)![](https://hxgqh.gitbooks.io/testautomization/content/assets/WechatIMG75.jpeg)3.启动Karma：

```
karma start karma.conf.js

```

![](https://hxgqh.gitbooks.io/testautomization/content/assets/WechatIMG76.jpeg)

## 参考资料： {#参考资料：}

[http://www.cnblogs.com/greatluoluo/p/5680738.html](http://www.cnblogs.com/greatluoluo/p/5680738.html)

