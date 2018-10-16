# angular

#### 作者：武超敏
#### 邮箱：wuchaomin@haomo-studio.com

```
更改历史

* 2018-01-27	高天阳     整理文档 补充$log
* 2018-01-23	武超敏     增加$q内容
* 2017-09-17	张飞       添加参考链接
* 2017-06-01    杨丽       初始化文档

```

## 1 历史、现状和发展

### 1.1 历史

**AngularJS**最初由**Misko Hevery**和**Adam Abrons**于2009年开发，后来成为了Google公司的项目。
**AngularJS**弥补了**HTML**在构建应用方面的不足，其通过使用标识符（directives）结构，来扩展**Web**应用中的**HTML**词汇，
使开发者可以使用**HTML**来声明动态内容，从而使得**Web**开发和测试工作变得更加容易。

### 1.2 简介

**AngularJS**是一个**JavaScript**框架。它可通过 `<script>` 标签添加到**HTML**页面。
**AngularJS**通过指令扩展了**HTML**，且通过表达式绑定数据到**HTML**。

### 1.3 特点

**AngularJS**有着诸多特性，最为核心的是：**MVVM**、模块化、自动化双向数据绑定、语义化标签、依赖注入等等。

## 2 安装和使用

### 2.1 安装angular

```
bower install --save-dev angular
```
### 2.2 常用的指令

* mg-app
* ng-model
* ng-controller
* ng-if
* ng-show
* ng-hide
* ng-repeat

### 2.3 服务

> 服务是一个对象或函数，对外提供特定的功能。

>> 内建服务: 
 
1. $location是对原生Javascript中location对象属性和方法的封装。  
2. $timeout&$interval对原生Javascript中的setTimeout和setInterval进行了封装。  
3. $filter在控制器中格式化数据。  
4. $log打印调试信息  
5. $http用于向服务端发起异步请求。  
6. 同时还支持多种快捷方式如$http.get()、$http.post()、$http.jsonp。 

angular提供了3种方法来创建并注册我们自己的service
- Factory,
- Service,
- Provider

#### 例子:

##### value   传递值

```
let app = angular.module("app",[]);
    app.value("name","yide");
    app.controller("myController",function($scope,name,){
         $scope.title = name;
})
```

##### service (new 实例化)

```
angular.module("app").service("ydserve",function(){
    this.name = "我是一个服务层";
});
    
```

##### factory  (执行实例化)

```
angular.module("app").factory("util",function(){
    return {
        sum:function(number1,number2){
            return number1 + number2;
        }
    };
});
```

#####  provider
(是唯一一种你可以传进 .config() 函数的 service。当你想要在 service 对象启用之前，先进行模块范围的配置，那就应该用 provider)

tips:得到的是$get() 执行之后的数据
```
angular.module("app").provider("ydprovider",function(){
    var _this = this;
    this.name = "provideryd";
    this.$get = function(){
        return {name:_this.name}
    }
});

```

### 2.4config
 tips:注意名字后面加Provider
 
 常用的$provide $compileProvider
```
angular.module("app").config(function(ydproviderProvider){
    ydproviderProvider.name = "config";
});

```

### 2.5directive

priority

template
 
返回函数的时候函数里面要返回string  (第二个形参看作元素)
 
返回对象
  
templateUrl

 ```angular2html
//缓存
angular.module("app").run(["$templateCache",function($templateCache){

    $templateCache.put("yd.html","<div><h1>Hi 我是缓存的</h1></div>")

}]);
angular.module("app").directive("yd",function(){

    let template  = {
        restrict:"E",
        templateUrl:"yd.html",
        replace:true
    }
    return template;
});
```
replace:是否替换原标签

transclude

restrict   E(元素),A(属性),C(类),M(注释) (默认为A)
 
E(元素)：`<directiveName></directiveName>  `

A(属性)：`<div directiveName='expression'></div>  `

C(类)： `<div class='directiveName'></div>  `

M(注释)：`<--directive:directiveName expression-->`

scope

false:同用一个scope
true:继承父scope如果自己有侧不用父scope的了
{}:不继承自己是单独的

隔离之后的双向绑定
{user: "="} 这个scope的user于父scope的user同步
{user: "@"} 父会改变它  它不会改变父
{fn: "&"} 拿到父的user这个函数

```
<div>Say：{{name}}<br>改变父scope的name：<input type="text" value="" ng-model="name"/></div> 
<div>隔离scope： 
    <div yd name="{{name}}"></div> 
</div> 
<div>隔离scope（不使用父scope {{name}}）： </div> 
<div yd name="name"></div> 

```

compile
  
link

 ### 2.6filter
 
```
angular.module("app").filter("reverse",function(){
    return function(text,flag){
        if(flag){
            return text.split("").reverse().join("");
        }
        return text;
    }
});
```


### 2.7$q

```
let promise = function(){
    let deferred =  $q.defer();
    $http({
        method:"GET",
        url:"https://jsonplaceholder.typicode.com/users/"+Math.ceil(Math.random()*10)
    }).then(function(data){
        deferred.resolve(data);
    },function(data){
        deferred.reject(data)
    });
    return deferred.promise;//返回promise对象
}

var p1 = promise();
p1.then(function(na){
    // alert(JSON.stringify(na));
},function(na){
    // alert(JSON.stringify(na));
}).finally(function(){
    // alert("反正我是最后执行的");
});

$q.all([promise(),promise(),p1]).then(function(result){
    result.forEach(function(v,i){
        console.log(v.data.name);

    });
});

```
#### 2.7.1$q.all的嵌套

函数1、2使用$q执行异步操作，对结果进行操作并执行函数5，
函数3、4使用$q执行异步操作，对结果进行操作并执行函数6，
函数5、6使用$q执行异步操作，对结果进行操作。

```

iWantResolve = true;//判断条件
function promise1() {
    var deferred = $q.defer();
    $timeout(function () {
        if (iWantResolve) {
            deferred.resolve("promise1 resolved");
        } else {
            deferred.reject("promise1 reject");
        }
    }, 500);
    return deferred.promise;
}

function promise2() {
    var deferred = $q.defer();
    $timeout(function () {
        if (iWantResolve) {
            deferred.resolve("promise2 resolved");
        } else {
            deferred.reject("promise2 reject");
        }
    }, 500);
    return deferred.promise;
}

function promise3() {
    var deferred = $q.defer();
    $timeout(function () {
        if (iWantResolve) {
            deferred.resolve("promise3 resolved");
        } else {
            deferred.reject("promise3 reject");
        }
    }, 500);
    return deferred.promise;
}

function promise4() {
    var deferred = $q.defer();
    $timeout(function () {
        if (iWantResolve) {
            deferred.resolve("promise4 resolved");
        } else {
            deferred.reject("promise4 reject");
        }
    }, 500);
    return deferred.promise;
}

function promise5() {
    var deferred = $q.defer();
    $timeout(function () {
        if (iWantResolve) {
            deferred.resolve("promise5 resolved");
        } else {
            deferred.reject("promise5 reject");
        }
    }, 500);
    return deferred.promise;
}

function promise6() {
    var deferred = $q.defer();
    $timeout(function () {
        if (iWantResolve) {
            deferred.resolve("promise6 resolved");
        } else {
            deferred.reject("promise6 reject");
        }
    }, 500);
    return deferred.promise;
}

var q = [];
var deferred5 = $q.defer();
var deferred6 = $q.defer();
$q.all([promise1(), promise2()])//执行promise1(), promise2()后，执行promise5()
.then(function (dataArr) {
    console.log(dataArr);//对promise1(), promise2()的结果进行操作
    promise5().then(function(data){
        deferred5.resolve("promise5 resolved-----");
    });
}, function (err) {
    console.log("$q.all: ", err)
});
q.push(deferred5.promise);//将promise5()的结果push到q数组中
$q.all([promise3(), promise4()])//执行promise3(), promise4()后，执行promise6()
.then(function (dataArr) {
    console.log(dataArr);//对promise3(), promise4()的结果进行操作
    promise6().then(function(data){
        deferred6.resolve("promise6 resolved-----");
    });
}, function (err) {
    console.log("$q.all: ", err)
});
q.push(deferred6.promise);//将promise6()的结果push到q数组中
$q.all(q)//运行q
.then(function (dataArr) {
    console.log(dataArr);
}, function (err) {
    console.log("$q.all: ", err)
});

```

#### 2.7.2$q原生(只为方便理解，不是实际的原生)

```
  function Promiesyd(callback){
    var vmy = this;
    vmy.flag = false;//标记是否进去resolve
    vmy.flagerr = false;//标记是否进入reject
    vmy.data;//存储成功时的数据
    vmy.dataerr;//存储失败时的数据
    var resolve = function(data2){	//5.执行成功函数,注入数据
        vmy.flag = true;
        vmy.data = data2;
    }
    var reject = function(data2){
        vmy.flagerr = true;
        vmy.dataerr = data2;
    }
    callback?callback(resolve,reject):'';	//3.给匿名函数注入数据resolve,reject
    this.then = function(success,err){		//7.监听异步是否执行完了,
        var intervalx =  setInterval(function(){
            if(vmy.flag){
                success(vmy.data);
                clearInterval(intervalx);
            }
            if(vmy.flagerr){
                err(vmy.dataerr);
                clearInterval(intervalx);
            }
        },50);
    }
  }

  var istrue = true;
  function q1(){
    return new Promiesyd(function(resolve,reject){ //1.new Promies  2.传递匿名函数，
        $timeout(function() {				//4.调用注入进来的resolve,reject
            if(istrue){
                resolve("异步执行成功1！！！");
            }else{
                reject("异步执行失败1！！");
            }

        }, 3000);
    });
  }

  q1()
  .then(function(data){		//6.调用then方法
    console.log(data);
  },function(data){
    console.log(data);
  })

```
#### 2.7.3$q.all原生(只为方便理解，不是实际的原生。q1()、q2()的实现参考$q原生)

```
  function allyd(promiesArr){
    var flag  = false;//判断数组是否为空 即：是否进for循环
    var flagAll  = false;//所有的promies是否执行完成
    var dataArr = [];//存放执行后的promies数据
    var intervalx1 =  setInterval(function(){     //2.监听数组存在并执行完成
        for(var i = 0;i < promiesArr.length;i++){
            flag = true;
            // console.log(promiesArr[i].flag);
            if(promiesArr[i].flag){
                dataArr.push(promiesArr[i].data);
                promiesArr.splice(i,1);
                i--;
            }
        }
        if(flag&&promiesArr.length==0){   //数组存在并执行完成，清除定时器
            flagAll = true;
            clearInterval(intervalx1);
        }
    },50);
    var obj = {};
    obj.then=function(success){
        var intervalx2 =  setInterval(function(){  //4.监听是否可以执行.then()
            // console.log("xx");
            if(flagAll){
                success?success(dataArr):'';
                clearInterval(intervalx2);
            }
        },50);
    };
    return obj;
  }

  allyd([q1(),q2()])    //1.addyd()的调用
  .then(function(data){   //3.执行.then()
    console.log(data);
  });

```
 
### 2.8 ui-router
 
 $stateProvider
 
### 2.9 $log

```
// 使用日志服务  
App.controller('DemoController', ['$log', function ($log) {  

    $log.info('普通信息');  
    
    $log.warn('警告信息');  
    
    $log.error('错误信息');  
    
    $log.log('打印信息');  
    
    $log.debug('调试信息');  

}]); 
```

## 参考资料

* [学习AngularJs:Directive指令用法（完整版）](http://www.jb51.net/article/83051.htm)
* [AngularJS 之 Factory vs Service vs Provider](http://www.oschina.net/translate/angularjs-factory-vs-service-vs-provider) 