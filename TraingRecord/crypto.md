# crypto使用

#### 作者：高天阳
#### 邮箱：13683265113@163.com

```
更改历史

* 2018-10-31        高天阳     初始化文档

```

## 1 简介

CryptoJS (crypto.js) 为 JavaScript 提供了各种各样的加密算法。目前已支持的算法包括：

* MD5
* SHA-1
* SHA-256
* AES
* Rabbit
* MARC4
* HMAC
* HMAC-MD5
* HMAC-SHA1
* HMAC-SHA256
* PBKDF2

散列/哈希

CryptoJS是一个纯javascript写的加密类库（下载），我们使用它只需要加入相关的引用即可：

散列/哈希示例1：

## 2 安装

### 2.1 使用npm

```
npm install crypto --save
```

### 2.2 使用cdn

```
<script src="http://cdn.bootcss.com/blueimp-md5/1.1.0/js/md5.min.js"></script>
```

## 3 使用

```
import crypto from "crypto"

let md5 = crypto.createHash("md5")
md5.update('aaa')
let password = md5.digest("hex") // 47bce5c74f589f4867dbd57e9ca9f808
```

## 5 最佳实践

## 参考资料

* [crypto官方文档](https://www.npmjs.com/package/crypto-browserify)
* [vue 实现MD5加密](https://blog.csdn.net/superKM/article/details/80956259)
* [vue中使用MD5加密](https://blog.csdn.net/take_up/article/details/77866306)
* [vue使用md5加密](https://www.cnblogs.com/muamaker/p/9082969.html)
