# FUSE-Angular前端框架项目初始化

#### 作者：高天阳
#### 邮箱：13683265113@163.com

```angular2html
更改历史

* 2017-11-21	高天阳	初始化文档

```

## 克隆、安装及启动

### 在项目中添加clone权限： 

![](/assets/Fuse/Fuse1.jpeg)
![](/assets/Fuse/Fuse2.jpeg)


### 克隆项目至本地：
```angular2html
git clone [项目克隆地址]

code:
git clone git@115.28.80.125:haomo/wechatgame.git
```

### 切换开发分支：
```angular2html
git branch -a   // 查看分支
git checkout dev    // 切换至dev分支
```

### 服务启动说明：

```angular2html
npm install // 安装服务器插件(若安装过慢或丢包，请使用cnom安装)
bower install // 安装依赖的插件  
```

### 服务启动：
```angular2html
gulp serve // 启动项目
```

## 目录结构、文件功能介绍

### 目录结构：

```angular2html
wechatgame/src/app/main/wegame/    编写代码存放目录
wechatgame/bower_components     插件依赖
wechatgame/node_modules     开发依赖
```
![](/assets/Fuse/Fuse3.jpeg)

### 主要文件及功能
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


## 初始化项目、配置路由

### 引入模块
![](/assets/Fuse/Fuse3.jpeg)


## 其他提示

### 引入ui-grid组件，为解决打包部署后框架文字变为韩文问题，在部署脚本写了替换css的命令。

### 开发分支：dev  
### 切换分支命令： 

``` angular2html
git checkout -b dev  
git branch --set-upstream dev remotes/origin/dev
```

### 安装插件：

查看插件是否存在于bower库

```angular2html
bower search [插件名称]
```

安装插件并存储于项目依赖

```angular2html
bower install [插件名称] --save

bower install [插件名称] -S
```

安装插件并存储于开发依赖

```angular2html
bower install [插件名称] --save-dev

bower install [插件名称] -D
```

### 打包项目：

```angular2html
gulp build 打包 
```

### 错误修复:

* 项目无法启动,报错提示如下图:

![](/assets/Fuse/nodeSassP1.png)
![](/assets/Fuse/nodeSassP2.png)

此问题需安装node-sass
```
npm install node-sass
```

[解决方法链接](http://blog.csdn.net/u010116861/article/details/51886550)

### 代码结构

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
