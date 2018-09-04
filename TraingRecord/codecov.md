# codecov {#84-codecov}

## 第一章 CodeCov介绍 {#第一章-codecov介绍}

### 1.1 codecov简介 {#11-codecov简介}

Codecov 是一款检测代码覆盖率的测试工具，目前支持 Java、Javascript、Kotlin、NodeJS、PHP、Python、Ruby、Scala、Objective、C、 Swift、Go、R、C、Lua、C++、Perl、Clojure、Rust、Coffeescript、Dart、Erlang、Ocaml、F\#、C\#/.Net、Haskell 等二十几种语言的代码覆盖率检测； 提高我们开发人员的代码质量。作用是将我们运行单测产生的结果文件上传到Codecov上进行可视化展示。

### 1.2 CodeCov特点 {#12-codecov特点}

* 浏览器扩展
* 拉请求评论
* 提交状态
* 合并报告
* 标志

## 第二章 Codecov的使用 {#第二章-codecov的使用}

### 2.1 浏览器扩展 {#21-浏览器扩展}

chrome浏览器打开[chrome://extensions/](chrome://extensions/)\(该网址需要翻墙\)；点击**获取更多扩展程序**,搜索codecov：

![](https://hxgqh.gitbooks.io/testautomization/content/assets/codecovExpSearch.png)

添加Codecov Extension到chrome；

检测安装成功，在github上搜索一个js项目，打开具体的js文件，在js代码的右上角多出来一个描述coverage的工具栏；



这样我们就成功安装了coverage浏览器扩展

### 2.2 关联github {#22-关联github}

* 在github上创建一个新的仓库，原先的仓库也可以使用
* 打开[codecov官网](https://codecov.io/)可以选择github/bitbuket/gitlab三种登录方式

  这里我们使用github登录进行入门实例，登录之后选择github的仓库：

  ![](https://hxgqh.gitbooks.io/testautomization/content/assets/codecovhome.png)![](https://hxgqh.gitbooks.io/testautomization/content/assets/codecoveChooseRep.png)![](https://hxgqh.gitbooks.io/testautomization/content/assets/getToken.png)

获取到私有项目token之后，我们的准备工作就完成了

### 2.3 下载安装codecov {#23-下载安装codecov}

codecov依赖于node环境，可以使用npm下载

```
$ npm install codecov --save-dev

```

### 2.4 codecov使用简例 {#24-codecov使用简例}

codecov配合其他的测试框架例如Istanbul+mocha、Mocha + JSCoverage、instanbul+Lab等等

本例使用istanbul+mocha来生成报告，然后使用codecov来生成在线报告

本文接istanbul来进行实例，实例详情见istanbul

公开项目使用`codecov`即可生成在线报告，私人的项目使用`codecov --token=[2.2获取的token]`

完成后浏览器打开生成的地址，可以看到生成的在线报告：

![](https://hxgqh.gitbooks.io/testautomization/content/assets/codereportOnline.png)

## 参考文档 {#参考文档}

* [https://codecov.io](https://codecov.io/)
* [前端测试工具集锦](https://sanwen8.cn/p/123ZgAW.html)



