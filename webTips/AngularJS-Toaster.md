# AngularJs-toaster-Angular提示弹框

#### 作者：高天阳
#### 邮箱：13683265113@163.com

```angular2html
更改历史

* 2017-11-26	高天阳	初始化文档

```

## 1 简介

### 1.1 简介

AngularJS Toaster是toastr非阻塞通知jQuery库的AngularJS端口。它需要AngularJS v1.2.6或更高版本以及CSS3转换的角动画。
那么toaster是什么呢。toaster是一款非常炫酷的提示插件，忍耐不住的人可以先去看特效

## 2 安装、使用

### 2.1 安装

* Npm安装

```angular2html
npm install --save angularjs-toaster
```

* Bower安装

```angular2html
bower install --save angularjs-toaster
```

![](/assets/AngularJs-toaster1.jpeg)

### 2.2 添加容器

* 添加提示框容器指令

```
<toaster-container></toaster-container>
```

![](/assets/AngularJs-toaster3.jpeg)

### 2.3 引入依赖

```angular2html
angular.module('main', ['toaster', 'ngAnimate'])
    .controller('myController', function($scope, toaster) {
        $scope.pop = function(){
            toaster.pop('info', "title", "text");
        };
    });
```

![](/assets/AngularJs-toaster2.jpeg)

### 2.4 使用

```angular2html
toaster.pop('info', "title", "text");
```

示例:
```angular2html
toaster.pop('success', "查询成功");
toaster.pop('error', "查询失败");
```

![](/assets/AngularJs-toaster4.jpeg)

## 参考资料

* [AngularJs-toaster插件NPM介绍](https://www.npmjs.com/package/angularjs-toaster)
* [angular-toaster 入坑记](http://blog.csdn.net/qq_26626113/article/details/53106688)