# angular {#98-angular}

#### angular是什么? {#angular是什么}

AngularJS 最初由Misko Hevery 和Adam Abrons于2009年开发，后来成为了Google公司的项目。AngularJS弥补了HTML在构建应用方面的不足，其通过使用标识符（directives）结构，来扩展Web应用中的HTML词汇，使开发者可以使用HTML来声明动态内容，从而使得Web开发和测试工作变得更加容易。

#### 安装angular {#安装angular}

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

参考文献：[http://www.oschina.net/translate/angularjs-factory-vs-service-vs-provider](http://www.oschina.net/translate/angularjs-factory-vs-service-vs-provider)

