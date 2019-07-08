# TypeScript

#### 作者：高天阳
#### 邮箱：13683265113@163.com

```
更改历史

* 2019-07-08	    高天阳	初始化文档

```

## 1 简介与优势

### 1.1 简介

TypeScript是由**微软开发**的，一个**JavaScript超集**，遵循**ES6标准**

> ES5、ES6、JavaScript、TypeScript相互关系是什么？

ES是客户端脚本语言的规范，ES5、ES6是这个规范的不同版本，JavaScript、TypeScript是两种客户端脚本语言，
JavaScript实现了ES5规范，TypeScript实现了ES6规范

### 1.2 优势

* 支持ES6规范
* 强大的IDE支持(错误提示、语法提示、重构)
* Angular2的开发语言

## 2 环境配置

* 什么是compiler？为什么需要compiler？

这是编译器，把TypeScript编译为JavaScript，使用原因类似babel的使用

* [在线compiler](https://www.tslang.cn/play/index.html)

* 本地compiler

```
npm i -g typescript
```

编写ts文件后，使用命令行，执行`tsc XX.ts`即可在同目录下获得`XX.js`文件

例如编写类

```javascript
export class Hello {}
```

## 3 概念、语法和特性

### 3.1 字符串新特性

* 多行字符串

```javascript
var content = `aaa
bbb
ccc`
```

* 字符串模板

```javascript
var myname = 'gao tianyang'

var getname = function() {
  return 'gao tianyang'
}
console.log(`hello ${myname}`)
console.log(`hello ${getname()}`)
```

```javascript
var myname = 'gao tianyang'

var getName = function() {
  return 'gao tianyang'
}
console.log(`<div>
<span>${myname}</span>
<span>${getName()}</span>
</div>`)
```

* 自动拆分字符串

```javascript
function test(template, name, age) {
  console.log(template)
  console.log(name)
  console.log(age)
}

var myname = "gao tianyang"

var getAge = function () {
  return 18
}

test`hello my name is ${myname}, i'm ${getAge()}`
```

### 3.2 参数新特性
