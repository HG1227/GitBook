# FUSE-Angular前端框架项目初始化

#### 作者：高天阳
#### 邮箱：13683265113@163.com

```angular2html
更改历史

* 2017-11-21	高天阳	初始化文档
* 2017-12-2 	高天阳	补充导航、工具栏配置

```

## 1 克隆、安装及启动

### 1.1 在项目中添加clone权限： 

![](/assets/Fuse/Fuse1.jpeg)
![](/assets/Fuse/Fuse2.jpeg)


### 1.2 克隆项目至本地：
```angular2html
git clone [项目克隆地址]

code:
git clone git@115.28.80.125:haomo/wechatgame.git
```

### 1.3 切换开发分支：
```angular2html
git branch -a   // 查看分支
git checkout dev    // 切换至dev分支
```

### 1.4 服务启动说明：

```angular2html
npm install // 安装服务器插件(若安装过慢或丢包，请使用cnom安装)
bower install // 安装依赖的插件  
```

### 1.5 服务启动：
```angular2html
gulp serve // 启动项目
```

## 2 目录结构、文件功能介绍

### 2.1 目录结构：

```angular2html
wechatgame/src/app/main/wegame/     编写代码存放目录
wechatgame/src/app/navigation/      框架导航配置
wechatgame/src/app/toolbar/         框架工具栏配置
wechatgame/bower_components         插件依赖
wechatgame/node_modules             开发依赖
```
![](/assets/Fuse/Fuse3.jpeg)
![](/assets/Fuse/Fuse19.jpeg)

### 2.2 主要文件及功能

* 项目主体

```angular2html
index.route.js   配置起始页面
index.module.js   配置项目目录
wechatgame/src/app/main/wegame/sample.module.js    toolbar配置文件
wechatgame/src/app/main/wegame/customer/customer.module.js    路由配置文件
wechatgame/src/app/main/wegame/customer/XXX.html    具体页面文件
wechatgame/src/app/main/wegame/customer/XXX.js    具体页面路由文件
```

![](/assets/Fuse/Fuse4.jpeg)
![](/assets/Fuse/Fuse5.jpeg)
![](/assets/Fuse/Fuse6.jpeg)
![](/assets/Fuse/Fuse7.jpeg)
![](/assets/Fuse/Fuse8.jpeg)
![](/assets/Fuse/Fuse9.jpeg)
![](/assets/Fuse/Fuse10.jpeg)

* 导航栏

```angular2html
wechatgame/src/app/navigation/  导航配置
wechatgame/src/app/navigation/navigation.module.js   导航路由配置
wechatgame/src/app/navigation/navigation.controller.js   工具栏控制器配置
wechatgame/src/app/navigation/XXX/layouts   框架导航页面不同样式布局方案
```

![](/assets/Fuse/Fuse20.jpeg)

> 一般情况下 只会修改页面样式 此次还修改了控制器 增加了一个打开关闭判定

![](/assets/Fuse/Fuse22.jpeg)
![](/assets/Fuse/Fuse23.jpeg)

* 工具栏

```angular2html
wechatgame/src/app/toolbar/         工具栏配置
wechatgame/src/app/toolbar/toolbar.module.js   工具栏路由配置
wechatgame/src/app/toolbar/toolbar.controller.js   工具栏控制器配置
wechatgame/src/app/toolbar/XXX/layouts   工具栏页面不同样式布局方案
```

![](/assets/Fuse/Fuse21.jpeg)

> 工具栏主要包括:LOGO、下拉列表、搜索、国际化、更多

![](/assets/Fuse/Fuse26.jpeg)

> 修改了工具栏LOGO内容、登录用户姓名 注释了下拉栏多余内容、国际化、更多

![](/assets/Fuse/Fuse24.jpeg)
![](/assets/Fuse/Fuse25.jpeg)
![](/assets/Fuse/Fuse27.jpeg)

### 2.3 安装restangular并注入

安装restangular插件

```angular2html
bower install --save restangular
```
![](/assets/Fuse/Fuse15.jpeg)

在项目路由配置文件引入restangular

![](/assets/Fuse/Fuse16.jpeg)

在模块路由引入restangular

![](/assets/Fuse/Fuse18.jpeg)

在页面路由引入restangular

![](/assets/Fuse/Fuse17.jpeg)

## 3 常见问题及处理

### 3.1 模块加载失败

* 报错提示：路由配置出现问题

![](/assets/Fuse/Fuse11.jpeg)
![](/assets/Fuse/Fuse12.jpeg)

* 处理方法：页面路由需配置为模块的路由

![](/assets/Fuse/Fuse13.jpeg)

### 3.2 Sass安装失败报错

* 报错提示：项目无法启动,报错提示如下图

![](/assets/Fuse/nodeSassP1.png)
![](/assets/Fuse/nodeSassP2.png)

* 处理方法1：此问题需安装node-sass

```angular2html
npm install node-sass
```

[解决方法链接](http://blog.csdn.net/u010116861/article/details/51886550)

* 处理方法2：此问题需查看node版本(过高或过低均会影响Sass安装 建议node-6.X.X版本)

### 3.3 bower、gulp命令不是内部或外部可识别的命令

* npm安装bower、gulp成功，但bower install、gulp serve却提示命令不是内部或外部可识别的命令

* 处理方法：全局安装bower、gulp

```angular2html
npm install bower -g
npm install gulp -g
```

### 3.4 配置restangular失败

* 报错提示：

![](/assets/Fuse/Fuse14.jpeg)

* 处理方法：模块路由也需要注入restangular

![](/assets/Fuse/Fuse18.jpeg)

## 4 其他常用命令提示

### 4.1 引入ui-grid组件，为解决打包部署后框架文字变为韩文问题，在部署脚本写了替换css的命令。

### 4.2 切换分支命令(开发分支：dev)

``` angular2html
git checkout -b dev  
git branch --set-upstream dev remotes/origin/dev
```

### 4.3 安装插件：

* 查看插件是否存在于bower库

```angular2html
bower search [插件名称]
```

* 安装插件并存储于项目依赖

```angular2html
bower install [插件名称] --save

bower install [插件名称] -S
```

* 安装插件并存储于开发依赖

```angular2html
bower install [插件名称] --save-dev

bower install [插件名称] -D
```

### 4.4 打包项目：

```angular2html
gulp build 打包 
```

## 5 代码结构

```angular2html
vm.setSearchParams  = function(resetFlag){
  var deferred = $q.deferred();

  $q.all([1, 2]).then(function(values){
    vm.search.filters = {
      'table': {
        'column': {
          'in': values[0]
        }
      }
    }
  }, function(err){

  });

  Restangular().then(function(res){
    deferred.resolve(res.data);
  }, function(err){
    deferred.reject();
  });

  return deferred.promise;
};

vm.search = function(){
  vm.setFilters().then(function(data){
    vm.process(data);
  }, function(err){
    console.log(err);
  });

  Restangular().then(function(res){
    vm.process(data);
  })
};

vm.process = function(data){

};
```

```angular2html
vm.item = {};

vm.loadItem = function(id){
  Restangular().then(function(res){
    vm.item = res.data;
  })
};

vm.clearBeforeUpdate = function(){

};

vm.updateItem = function(){
  vm.clearBeforeUpdate();
  Restangular().post()
};

vm.columnOnChange = function(value){

};
```
