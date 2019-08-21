# Yeoman的使用

> Yeoman是一个通用的脚手架工具,允许任何的app

### Yeoman由哪几部分组成

1. YO:是yeoman命令行工具
1. grunt:用来搭建,预览和测试你的项目
1. bower:用来管理项目的工具,你可以不必手动下载前后端函数库

### 操作步骤

* 必备的软件:
    * node.js
    * npm
    * git

* 安装yeoman工具箱:
```
npm install -g yo bower grunt-cli
```

* 安装生成器:
```
npm install -g generator-[name]
```

* 创建文件夹并进入:

* 在文件中使用生成器:
```
yo [name]
```

* 配置生成器:

* 开启服务器:
```
grunt serve
```

### 实战——angular

* 安装yeoman工具箱:
```
npm install -g yo bower grunt-cli
```

* 确认yeoman安装工完毕:
```
yo -version && bower -version && grunt-cli -version
```

* 安装angularJs生成器:
```
npm install -g generator-angular
```

* 创建一个项目文件夹:
```
mkdir yeoAngular && cd yeoAngular
```

* 运行生成器:
```
yo 选择 angular / yo angular
```

* 配置生成器

* 开启服务器:
```
grunt serve
```