# Swagger {#swagger}

## 第一章 Swagger介绍 {#第一章-swagger介绍}

## 1.1.Swagger 介绍及历史 {#11swagger-介绍及历史}

Swagger：是一个规范和完整的框架，可以用于生成、描述、调用和可视化 RESTful 风格的 Web 服务，总体目标是使客户端和文档系统与服务器以同样的速度进行更新。Swagger倾向于在线测试接口和数据。并且这是一个完全开源的项目，并且它也是一个基于Angular的成功案例，我们可以下载源码并自己部署它，也可以修改它或集成到我们自己的软件中。

Swagger的创始人： Tony Tam

2009年Swagger框架启动，但是在当时Swagger API框架只是在Reverb内部开发的一个项目 ；

2011-10-11 1.0.1版本；2013-03-08 1.0.13；

2014年5月 Swagger的开放工作小组 成立；

Swagger 2.0.24在2014年9月12日正式发布；

Swagger规范未来的发展将由SmartBear负责，这是一家位于马萨诸塞州的软件工具公司。

2016-07-20 2.1.5版本；2016-10-14 2.2.6版本；

## 1.2相关工具 {#12相关工具}

API Blueprint：提供跨越API整个周期的工具，这样可以和别人讨论你的API，可以产生自动文档或一个测试案例。它是使用Markdown来定义API的，Markdown相比RAML、JSON门槛又降低了一大截。同时API Blueprint与Swagger、RAML一样也能提供可视化的文档界面与Mock Server的功能。不过其Mock能力比较弱。

RAML：是一种RESTful API 建模语言\(RESTful API Modeling Language :RAML\)， 是对 RESTful API的一种简单和直接的描述 ， 它鼓励重用 激活发现和模式分享，定位在最佳实践的最优实现。它是一种让人们易于阅读并且能让机器对特定的文档能解析的语言。RAML 是基于 YAML,能帮助设计 RESTful API 和鼓励对API的发掘和重用,依靠标准和最佳实践从而编写更高质量的API。通过RAML定义,因为机器能够看得懂,所以可以衍生出一些附加的功能服务,像是解析并自动生成对应的客户端调用代码、服务端代码 结构, API说明文档

## 第二章：Swagger安装及使用 {#第二章：swagger安装及使用}

### 2.1 Swagger Editor安装 {#21-swagger-editor安装}

需要下载一个Swagger Editor，也可以直接使用在线版本[http://editor.swagger.io/。](http://editor.swagger.io/%E3%80%82)

现在地址：`git clone https://githup.com/swagger-api/swagger-editor.git`

下载完成后进行本地配置（前提是已经安装好了Node.js），命令如下：

```
1.cd swagger-editor

2.npm install -g http-server

3.http-server （默认的是：8080端口）

4.http-server -p 7000 可以修改端口（临时）

```

效果图：![](https://hxgqh.gitbooks.io/haomotraining/content/assets/Swagger1.jpeg)![](https://hxgqh.gitbooks.io/haomotraining/content/assets/Swagger2.jpeg)默认端口：![](https://hxgqh.gitbooks.io/haomotraining/content/assets/Swagger3.jpeg)修改后的端口：![](https://hxgqh.gitbooks.io/haomotraining/content/assets/Swagger4.jpeg)![](https://hxgqh.gitbooks.io/haomotraining/content/assets/Swagger5.jpeg)

### 2.2 Swagger-UI的安装 {#22-swagger-ui的安装}

现在地址：`git clone https://githup.com/swagger-api/swagger-ui.git`

Swagger UI的本地配置：

1,创建一个 node目录

`mkdir node`

2.初始化 node，创建package.json

~ &gt;`cd node`

~ &gt;`node >npm init`

3.安装express

~ &gt;`node >npm install express --save`

效果图：![](https://hxgqh.gitbooks.io/haomotraining/content/assets/Swagger6.jpeg)

4 .创建index.js

~ &gt;`node > vim index.js`

将一下代码复制到index.js中：

```
var express = require('express');

var app = express();

app.use('/static', express.static('public'));

app.get('/', function (req, res) {

    res.send('Hello World!');

});

app.listen(5000, function () {

    console.log('Example app listening on port 5000!');

});

```

5.创建public文件夹：

~ &gt;`node > mkdir public`

**把Swagger-UI文件中dist目录下的文件全部复制到public中：**

效果图：![](https://hxgqh.gitbooks.io/haomotraining/content/assets/Swagger7.jpeg)

6.开启node

~ &gt;`node > node index.js`

打开浏览器输入：`localhost:3000/static/index.html`

### 2.3 Swagger参数介绍 {#23-swagger参数介绍}

![](https://hxgqh.gitbooks.io/haomotraining/content/assets/Swagger8.jpeg)

```
get/post/delete/ 是指这个接口对应的请求方式

tags 当前接口的分类

summary 是对这个接口进行的一个总体描述

```

![](https://hxgqh.gitbooks.io/haomotraining/content/assets/Swagger9.jpeg)

```
description：对接口的描述

parameters: 接口需要传递的参数

- name: X-Auth-Token 参数的名字

in: header 他的值:header、path、formData Query body

description: /auth接口获取的token

required: true 两个值:true、false；true为必填项，false为非必填项

type: string 参数格式

```

## 参考文档 {#参考文档}

知乎网比较详细的Swagger介绍：[https://zhuanlan.zhihu.com/p/21353795](https://zhuanlan.zhihu.com/p/21353795)

RESTful架构风格介绍：[http://www.cnblogs.com/chinajava/p/5871305.html](http://www.cnblogs.com/chinajava/p/5871305.html)

[http://www.cnblogs.com/whitewolf/p/4686154.html](http://www.cnblogs.com/whitewolf/p/4686154.html)

swagger ；[https://topbitdu.gitbooks.io/swagger-document-convention/content/](https://topbitdu.gitbooks.io/swagger-document-convention/content/)

Swagger-UI 的官方地址：[http://swagger.wordnik.com](http://swagger.wordnik.com/)

Github上的项目地址：[https://github.com/wordnik/swagger-ui](https://github.com/wordnik/swagger-ui)

官方提供的demo地址：[http://petstore.swagger.wordnik.com/](http://petstore.swagger.wordnik.com/)

官方：[https://github.com/adrianbk/swagger-springmvc-demo](https://github.com/adrianbk/swagger-springmvc-demo)

Swagger的发展史：[http://www.infoq.com/cn/articles/swagger-interview-tony-tam](http://www.infoq.com/cn/articles/swagger-interview-tony-tam)

Swagger本地设置：[http://www.jianshu.com/p/d6626e6bd72c](http://www.jianshu.com/p/d6626e6bd72c)

