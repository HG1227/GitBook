### 课堂笔记

简介

[https://www.douban.com/note/314200231/](https://www.douban.com/note/314200231/)

Pm2startpm2.js--watch

Pm2startupOR自启动

Pm2list监听状态

# PM2 {#pm2}

pm2官方文档：&lt;[http://pm2.keymetrics.io/docs/usage/quick-start/&gt;](http://pm2.keymetrics.io/docs/usage/quick-start/&gt);

# 简单教程 {#简单教程}

首先需要安装pm2：

```
npm install -g pm2
```

运行：\#实时监控app.js的方式启动，当app.js文件有变动时，pm2会自动reload

```
pm2 start app.js --watch
```

开机自启:

```
pm2 startup
pm2 save
```

初次安装并运行，会有一个高大上的界面：

![](http://upload-images.jianshu.io/upload_images/31920-a87d9f022b1bad3b.png?imageMogr2/auto-orient/strip|imageView2/2/w/1240)

直接我们介绍过[forever](http://www.jianshu.com/p/82a64aee0710)，那么pm2与forever相比较有哪些高大上的功能呢？我们看一下对比表格：

| Feature | Forever | PM2 |
| :--- | :--- | :--- |
| Keep Alive | ✔ | ✔ |
| Coffeescript | ✔ |  |
| Log aggregation |  | ✔ |
| API |  | ✔ |
| Terminal monitoring |  | ✔ |
| Clustering |  | ✔ |
| JSON configuration |  | ✔ |

我们可以很直观的看出，pm2相比较Forever，功能更加强大一些。

# 查看运行状态 {#查看运行状态}

我们可以通过简单的命令查看应用的运行状态：

```
pm2 list
```

效果如下：

![](http://upload-images.jianshu.io/upload_images/31920-460416a1351fa20b.png?imageMogr2/auto-orient/strip|imageView2/2/w/1240)

> ANodeBlog应用正在运行，pid为31480，并且占用内存为89.113 MB。

## 追踪资源运行情况 {#追踪资源运行情况}

```
pm2 monit
```

会看到应用资源的实时运行情况

![](http://upload-images.jianshu.io/upload_images/31920-d9b61b829f16f467.png?imageMogr2/auto-orient/strip|imageView2/2/w/1240)

## 查看应用详细部署状态 {#查看应用详细部署状态}

如果我们想要查看一个应用详细的运行状态，比如`ANodeBlog`的状态，可以运行：

```
pm2 describe 3
```

> “3”是指App Id。

结果如下：

![](http://upload-images.jianshu.io/upload_images/31920-7d990f92952b28c3.png?imageMogr2/auto-orient/strip|imageView2/2/w/1240)

# 查看日志 {#查看日志}

```
pm2 logs
```

系统会打印出详细的logs。

# 重启应用 {#重启应用}

```
pm2 restart appId
```

# 停止应用 {#停止应用}

想要终止应用，只需要运行：

```
pm2 stop app.js
```

# 强健的API {#强健的api}

在项目中运行：（显示部署的服务器信息和程序的信息）

```
pm2 web
```

然后浏览器访问&lt;[http://localhost:9615&gt;](http://localhost:9615&gt/); 你会有惊喜！

# 预定义运行配置文件 {#预定义运行配置文件}

我们可以预定义一个配置文件，然后制定运行这个配置文件，比如我们定义一个文件`process.json`，内容如下：

```
{
"apps": [
{
"name": "ANodeBlog",
"script": "bin/www",
"watch": "../",
"log_date_format": "YYYY-MM-DD HH:mm Z"
}
]
}
```

然后可以通过

```
pm2 start process.json
```

运行这个App。

# 总结 {#总结}

常用命令总结如下：

1. 安装pm2

```
npm install -g pm2
```

1. 启动应用

```
pm2 start app.js
```

1. 列出所有应用

```
pm2 list
```

1. 查看资源消耗

```
pm2 monit
```

1. 查看某一个应用状态

```
pm2 describe [app id]
```

1. 查看所有日志

```
pm2 logs
```

1. 重启应用

```
pm2 restart [app id]
```

1. 停止应用

```
pm2 stop [app id]
```

1. 开启api访问

```
pm2 web
```

更多pm2内容请参考官方文档：&lt;[http://pm2.keymetrics.io/docs/usage/quick-start&gt;](http://pm2.keymetrics.io/docs/usage/quick-start&gt);

坚持把简单的事情做好就是不简单，坚持把平凡的事情做好就是不平凡。所谓成功，就是在平凡中做出不平凡的坚持。

