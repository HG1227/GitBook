# ngclipboard-Angular复制到剪贴板

#### 作者：高天阳
#### 邮箱：13683265113@163.com

```
更改历史

* 2017-11-26	高天阳	初始化文档

```

## 1 简介、特点

### 1.1 简介

ngclipboard使用angularjs指令将文本复制到剪贴板而不使用flash

### 1.2 特点

复制文本到剪贴板应该不难。它不需要几十个步骤来配置或加载数百个KB。但最重要的是，它不应该依赖于Flash或任何臃肿的框架。

## 2 安装、使用

### 2.1 安装

* Npm安装

```
npm install ngclipboard --save
```

* Bower安装

```
bower install ngclipboard --save
```

![](/assets/ngclipboard1.jpeg)

### 2.2 引入依赖

```
var myApp = angular.module('app', ['ngclipboard']);
```

![](/assets/ngclipboard2.jpeg)

### 2.3 使用

* 可是使用id来加载标签里面的内容

```
data-clipboard-target="#foo"
```

示例:

```
<!-- Target -->
<input id="foo" value="https://github.com/sachinchoolur/ngclipboard.git">

<!-- Trigger -->
<button class="btn" ngclipboard data-clipboard-target="#foo">
    <img src="assets/clippy.svg" alt="Copy to clipboard">
</button>
```

![](/assets/ngclipboard3.jpeg)

* 也可以获取值

```
data-clipboard-text=""
```

示例:

```
<input type="text" ng-model="$ctrl.copyText" />
<button class="btn btn-primary" uib-tooltip="复制成功" tooltip-popup-close-delay='1000' tooltip-trigger="'focus'" ngclipboard data-clipboard-text='{{$ctrl.copyText}}'>
    复制
</button>
```

## 参考资料

* [angular复制插件ngclipboard](https://segmentfault.com/a/1190000009382333)
* [ngclipboard插件NPM介绍](http://angular-js.in/ng-clipboard/)
