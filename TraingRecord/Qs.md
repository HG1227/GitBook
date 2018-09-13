# Qs

#### 作者：高天阳
#### 邮箱：13683265113@163.com

```
更改历史

* 2018-09-12	    高天阳	初始化文档

```

## 1 简介

qs 是一个增加了一些安全性的查询字符串解析和序列化字符串的库。

主要维护者：[Jordan Harband](https://github.com/ljharb)

在QS模块最初创建和维护[TJ Holowaychuk](https://github.com/tj/node-querystring)。

## 2 安装与使用

### 2.1 安装

#### 2.1.1 npm

qs是一个npm仓库所管理的包,可通过npm命令进行安装. 

```
npm install qs
```

#### 2.1.2 script引入

qs是一个npm仓库所管理的包,可通过npm命令进行安装. 

```
<script src="https://cdn.bootcss.com/qs/6.5.1/qs.min.js"></script>
```

[qs不同版本bootcdn链接](https://www.bootcdn.cn/qs/)

### 2.2 使用

### 2.3 示例

#### 2.3.1 qs.parse()

将URL解析成对象的形式

```
const Qs = require('qs');
let url = 'method=query_sql_dataset_data&projectId=85&appToken=7d22e38e-5717-11e7-907b-a6006ad3dba0';
Qs.parse(url);
console.log(Qs.parse(url));
```

如上面代码所示,输出结果如下: 

```
{
    method: 'query_sql_dataset_data',
    projectId: '85',
    appToken: '7d22e38e-5717-11e7-907b-a6006ad3dba0'
}
```

#### 2.3.2 qs.stringify()

将对象 序列化成URL的形式，以&进行拼接

```
const Qs = require('qs');
let obj= {
     method: "query_sql_dataset_data",
     projectId: "85",
     appToken: "7d22e38e-5717-11e7-907b-a6006ad3dba0",
     datasetId: " 12564701"
   };
Qs.stringify(obj);
console.log(Qs.stringify(obj));
```

如上面代码所示,输出结果如下: 

```
method=query_sql_dataset_data&projectId=85&appToken=7d22e38e-5717-11e7-907b-a6006ad3dba0&datasetId=12564701
```

那么当我们需要传递数组的时候，我们就可以通过下面方式进行处理： 

默认情况下，它们给出明确的索引，如下代码：

```
qs.stringify({ a: ['b', 'c', 'd'] });
// 'a[0]=b&a[1]=c&a[2]=d'
```

也可以进行重写这种默认方式为`false`

```
qs.stringify({ a: ['b', 'c', 'd'] }, { indices: false });
// 'a=b&a=c&a=d'
```

当然，也可以通过`arrayFormat`选项进行格式化输出，如下代码所示：

```
qs.stringify({ a: ['b', 'c'] }, { arrayFormat: 'indices' })
// 'a[0]=b&a[1]=c'
qs.stringify({ a: ['b', 'c'] }, { arrayFormat: 'brackets' })
// 'a[]=b&a[]=c'
qs.stringify({ a: ['b', 'c'] }, { arrayFormat: 'repeat' })
// 'a=b&a=c'
```

在这里需要注意的是，JSON中同样存在stringify方法，但是两者之间的区别是很明显的，如下所示：

```
const Qs = require('qs');
let obj= {
     uid: "cs11",
     pwd: "000000als",
     username: "cs11",
     password: " 000000als"
   };
Qs.stringify(obj);
console.log(JSON.stringify(param));
// '{"uid":"cs11","pwd":"000000als","username":"cs11","password":"000000als"}'
console.log(Qs.stringify(obj));
// 'uid=cs11&pwd=000000als&username=cs11&password=000000als'
```

如上所示，前者是采用JSON.stringify(param)进行处理，后者是采用Qs.stringify(param)进行处理的。

## 3 最佳实践

## 4 同类型技术比较

## 参考资料
   
* [npm-qs](https://www.npmjs.com/package/qs)
* [npm qs 模块(中文)](https://blog.csdn.net/sansan_7957/article/details/82227040)
* [通过script标签引入qs](https://blog.csdn.net/weixin_41769582/article/details/80063517)
* [qs.parse()、qs.stringify()使用方法](https://blog.csdn.net/suwu150/article/details/78333452)
* [qs.js - 更好的处理url参数](https://www.cnblogs.com/small-coder/p/9115972.html)