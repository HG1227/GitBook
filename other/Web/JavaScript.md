# JavaScript方面

#### 作者：高天阳
#### 邮箱：13683265113@163.com

```
更改历史

* 2019-08-09        高天阳     初始化文档

```

## 正则相关

```javascript
// 以下哪个能 str 能和 result 匹配
result = str.replace(/^\s+|\s+$/, '') // 去除首尾空格
// str = ' a b c ', result = 'a b c'
// str = ' a b c ', result = 'abc'
// str = ' a b c ', result = 'a b c '
// str = ' a b c ', result = ' a b c'
```

## dom 的操作，常用的有哪些，如何创建、添加、移除、移动、复制、查找节点？

- 创建 `createElement()`
- 添加 `appendChild()`
- 移除 `removeChild()`
- 移动 `replaceChild()`
- 复制 `cloneNode()`
- 查找节点 `getElementById()、getElementsByName()、getElementsByTagName()、querySelector()、querySelectorAll()`

```
querySelector() // 获取查找到的第一个
querySelectorAll() // 获取查找到的所有
document.querySelector("p")
document.querySelector(".example")
document.querySelector("a[target]")
```

## 闭包

```javascript
function foo () {
    var i = 0;
    return function () {
        console.log(i++)
    }
}
var f1 = foo()
var f2 = foo()
f1()    // 0
f1()    // 1
f2()    // 0
f1()    // 2
```

## 正则表达式 ^d+[^d]+ 能匹配下列哪个字符串？

- a.123
- b.123a
- c.d123
- d.123def
- e.d7d

> ^d+是以d字母开头并且一个或者多个d
> ^\d+才是是以数字开头并且一个或者多个数字
> [^d]+是非d字母一个或者多个


## 以下哪些是HTTP请求中浏览器缓存机制会用到的协议头？

- Last-Modified 标示这个响应资源的最后修改时间
- Etag web服务器响应请求时，告诉浏览器当前资源在服务器的唯一标识
- Referer 告诉服务器我来自于哪里
- Authorization 认证，http协议是无状态的，浏览器和web服务器之间可以通过cookie来身份识别, 桌面应用程序一般不会使用cookie, 
而是把 "用户名+冒号+密码"用BASE64编码的字符串放在http request 中的header Authorization中发送给服务端，来进行身份认证

## 关于HTTP协议头描述不正确的是()

- cookie是通过http请求正文传到服务器端
- cookie是保存在客户端的
- 服务器端可以读取客户端的**所有**cookie
- cookie是通过http请求报头传到服务器端

## 以下方案中，是不用于解决回调陷阱的是？

> 回调陷阱是指异步请求回调的层级嵌套，导致代码不可维护

- Promise
- Generator
- async // Generator的语法糖
- proxy

## 一次完整的HTTP事务过程

1. 域名解析
1. 发起TCP的3次握手
1. 建立TCP连接后发起http请求
1. 服务器响应http请求，浏览器得到html代码
1. 浏览器解析html代码，并请求html代码中的资源（如js、css、图片等）
1. 浏览器对页面进行渲染呈现给用户

## 手写一个闭包


## jQuery的$是什么，用原生js写一个链式调用


## this相关问题 apply、call、bind 部分函数、高阶函数


## 手写一个递归操作 将字符串翻转


## 二叉树的算法问题

