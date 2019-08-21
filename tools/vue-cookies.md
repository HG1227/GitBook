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
// require
var Vue = require('vue')
Vue.use(require('vue-cookies'))

// es2015 module
import Vue from 'Vue'
import VueCookies from 'vue-cookies'
Vue.use(VueCookies)
```

## 4 Api

设置 cookie

```
this.$cookies.config(expireTimes[,path])  // default: expireTimes = 1d , path=/
```

存储 cookie

```
this.$cookies.set(keyName, time)   //return this
```

获取 cookie

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

时间单位对照

| 缩写 | 含义 |
| :---: | :---: |
| y | 年 |
| m | 月 |
| d | 天 |
| h | 小时 |
| min | 分钟 |
| s | 秒 |

## 5 示例

```
this.$cookies.set("default_unit_second","input_value",1);            // 1 second after, expire
this.$cookies.set("default_unit_second","input_value",60 + 30);      // 1 minute 30 second after, expire
this.$cookies.set("default_unit_second","input_value",60 * 60 * 12); // 12 hour after, expire
this.$cookies.set("default_unit_second","input_value",60 * 60 * 24 * 30); // 1 month after, expire
```

```
this.$cookies.set("token","GH1.1.1689020474.1484362313","60s");  // 60 second after, expire
this.$cookies.set("token","GH1.1.1689020474.1484362313","30MIN");  // 30 minute after, expire, ignore case
this.$cookies.set("token","GH1.1.1689020474.1484362313","24d");  // 24 day after, expire
this.$cookies.set("token","GH1.1.1689020474.1484362313","4m");  // 4 month after, expire
this.$cookies.set("token","GH1.1.1689020474.1484362313","16h");  // 16 hour after, expire
this.$cookies.set("token","GH1.1.1689020474.1484362313","3y");  // 3 year after, expire
 
// input date string 
this.$cookies.set('token',"GH1.1.1689020474.1484362313", new Date(2017,03,13).toUTCString());
this.$cookies.set("token","GH1.1.1689020474.1484362313", "Sat, 13 Mar 2017 12:25:57 GMT ");
```

## 参考资料

* [npmjs说明](https://www.npmjs.com/package/vue-cookies)
* [vue之vue-cookies](https://www.cnblogs.com/s313139232/p/9341762.html)
 