# angular {#98-angular}

#### angular是什么? {#angular是什么}

AngularJS 最初由Misko Hevery 和Adam Abrons于2009年开发，后来成为了Google公司的项目。AngularJS弥补了HTML在构建应用方面的不足，其通过使用标识符（directives）结构，来扩展Web应用中的HTML词汇，使开发者可以使用HTML来声明动态内容，从而使得Web开发和测试工作变得更加容易。

#### 安装angular {#安装angular}

bower install --save-dev angular

#### 常用的指令 {#常用的指令}

mg-app

ng-model

ng-controller

ng-if

ng-show

ng-hide

ng-repeat

#### 服务 {#服务}

angular提供了3种方法来创建并注册我们自己的service

* Factory,
* Service,
* Provider

#### 例子: {#例子}

##### value 传递值 {#value---传递值}

```
    let app = angular.module("app",[]);
        app.value("name","yide");
        app.controller("myController",function($scope,name,){
             $scope.title = name;
    })

```

##### service \(new 实例化\) {#service-new-实例化}

```
    angular.module("app").service("ydserve",function(){
        this.name = "我是一个服务层";
    });

```

##### factory \(执行实例化\) {#factory--执行实例化}

```
    angular.module("app").factory("util",function(){
        return {
            sum:function(number1,number2){
                return number1 + number2;
            }
        };
    });

```

##### provider {#provider}

\(是唯一一种你可以传进 .config\(\) 函数的 service。当你想要在 service 对象启用之前，先进行模块范围的配置，那就应该用 provider\)

tips:得到的是$get\(\) 执行之后的数据

```
    angular.module("app").provider("ydprovider",function(){
        var _this = this;
        this.name = "provideryd";
        this.$get = function(){
            return {name:_this.name}
        }
    });

```

参考文献：[http://www.oschina.net/translate/angularjs-factory-vs-service-vs-provider](http://www.oschina.net/translate/angularjs-factory-vs-service-vs-provider)

##### config {#config}

tips:注意名字后面加Provider

常用的$provide $compileProvider

```
    angular.module("app").config(function(ydproviderProvider){
        ydproviderProvider.name = "config";
    });

```

##### directive {#directive}

　　priority

　　template

返回函数的时候函数里面要返回string \(第二个形参看作元素\)

返回对象

　　templateUrl

```
//缓存
    angular.module("app").run(["$templateCache",function($templateCache){

        $templateCache.put("yd.html","
<
div
>
<
h1
>
Hi 我是缓存的
<
/h1
>
<
/div
>
")

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

　　restrict E\(元素\),A\(属性\),C\(类\),M\(注释\) \(默认为A\)

```
 E(元素)：
<
directiveName
>
<
/directiveName
>
  
 A(属性)：
<
div directiveName='expression'
>
<
/div
>
  
 C(类)： 
<
div class='directiveName'
>
<
/div
>
  
 M(注释)：
<
--directive:directiveName expression--
>
```

　　scope

```
false:同用一个scope
true:继承父scope如果自己有侧不用父scope的了
{}:不继承自己是单独的

隔离之后的双向绑定
{user: "="} 这个scope的user于父scope的user同步
{user: "@"} 父会改变它  它不会改变父
{fn: "
&
"} 拿到父的user这个函数





<
div
>
Say：
<
br
>
改变父scope的name：
<
input type="text" value="" ng-model="name"/
>
<
/div
>
<
/div
>
<
div
>
隔离scope： 
 
<
div yd name=""
>
<
/div
>
<
/div
>
<
div
>
隔离scope（不使用父scope ）： 
 
<
div yd name="name"
>
<
/div
>
```

　　compile

　　link

参考文献：[http://www.jb51.net/article/83051.htm](http://www.jb51.net/article/83051.htm)

##### 服务
> 服务是一个对象或函数，对外提供特定的功能。  
内建服务: 
 
1. $location是对原生Javascript中location对象属性和方法的封装。  
2. $timeout&$interval对原生Javascript中的setTimeout和setInterval进行了封装。  
3. $filter在控制器中格式化数据。  
4. $log打印调试信息  
5. $http用于向服务端发起异步请求。  
6. 同时还支持多种快捷方式如$http.get()、$http.post()、$http.jsonp。  


##### filter {#filter}

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

##### $q {#q}

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

##### ui-router {#ui-router}

$stateProvider

##### $log {#log}

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