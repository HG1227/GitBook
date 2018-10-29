# vue-cookies使用

#### 作者：高天阳
#### 邮箱：13683265113@163.com

```
更改历史

* 2018-10-29        高天阳     初始化文档

```

## 1 简介

一个简单的Vue.js插件，用于处理浏览器cookie

## 2 安装

```
npm install vue-cookies --save
```

## 3 使用

```
import Vue from 'Vue'
import VueCookies from 'vue-cookies'
Vue.use(VueCookies)
```

## 4 Api

设置 cookie：

```
this.$cookies.set(keyName, time)   //return this
```

获取cookie

```
this.$cookies.get(keyName)       // return value
```

删除 cookie

```
this.$cookies.remove(keyName)   // return  false or true , warning： next version return this； use isKey(keyname) return true/false,please
```

查看一个cookie是否存在（通过keyName）

```
this.$cookies.isKey(keyName)        // return false or true
```

获取所有cookie名称

```
this.$cookies.keys()  // return a array
```
