# md5使用

#### 作者：高天阳
#### 邮箱：13683265113@163.com

```
更改历史

* 2018-10-30        高天阳     初始化文档

```

## 1 简介

## 2 安装

## 3 配置

## 4 示例

```
import crypto from 'crypto'
export default {
  name: 'HelloWorld',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App'
    }
  },
  mounted(){
    this.getmd5("aaa");
  },
  methods:{
    getmd5(str){
            var a;
            var md5 = crypto.createHash("md5");
            //update("中文", "utf8")
            md5.update(str);
            var a = md5.digest('hex');
            console.log(a);
            //47bce5c74f589f4867dbd57e9ca9f808
            return a;
        }
  }
}
```

## 5 最佳实践

## 参考资料

* [js-md5官方文档](https://www.npmjs.com/package/js-md5)
* [在vue项目中使用md5加密](https://www.jianshu.com/p/f218555cb593)
* [如何在vue项目中使用md5加密](https://yq.aliyun.com/ziliao/553771)
* [如何在vue项目中使用md5加密](https://blog.csdn.net/skyblacktoday/article/details/80255348)
* [crypto官方文档](https://www.npmjs.com/package/crypto-browserify)
* [vue 实现MD5加密](https://blog.csdn.net/superKM/article/details/80956259)
* [vue中使用MD5加密](https://blog.csdn.net/take_up/article/details/77866306)
* [vue使用md5加密](https://www.cnblogs.com/muamaker/p/9082969.html)
* [如何在vue项目中使用md5.js及base64.js](https://blog.csdn.net/qq_35844177/article/details/70597597)
