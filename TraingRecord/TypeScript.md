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

微软+google

## 2 环境配置

* 什么是compiler？为什么需要compiler？

compiler是编译器，把TypeScript编译为JavaScript，使用原因类似babel的使用

* [在线compiler](https://www.tslang.cn/play/index.html)

* 本地compiler

```
npm i -g typescript
```

编写ts文件后，使用命令行，执行`tsc XX.ts`即可在同目录下获得`XX.js`文件

例如编写类

```typescript
export class Hello {}
```

当我们使用IDE时，其会充当compiler，帮助我们进行编译，并把ts文件变更为js文件

## 3 概念、语法和特性

### 3.1 字符串新特性

* 多行字符串

```typescript
var content = `aaa
bbb
ccc`
```

* 字符串模板

```typescript
var myname = 'gao tianyang'

var getname = function() {
  return 'gao tianyang'
}
console.log(`hello ${myname}`)
console.log(`hello ${getname()}`)
```

```typescript
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

```typescript
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

* 参数类型：在参数名称后面使用冒号来制定参数的类型

```typescript
var myname: string  = "gao tianyang"
myname = 13

var alias = "wang zhiwei"
alise = 13

var alias: any = "wang zhiwei"
alise = 13

var age: number = 13

var man: boolean = true

function test() : void {
  return ""
}
test()

function test2() : string {
  return ""
}
test2()

function test3(name: string) : string {
  return ""
}
test3(13)

class Person {
  name: string;
  age: number;
}

var zhangsan: Person = new Person ()
zhangsan.name = ""
zhangsan.age = 18
```

* 默认参数：在参数声明后面用等号来指定参数的默认值

```typescript
var myname: string = "gao tiangyang"

function test(a:string, b:string, c:string) {
    console.log(a)
    console.log(b)
    console.log(c)
}
test("x")
test("x","y","z")

// 注意带默认值的参数需要放置在最后
function test2(a:string, b:string, c:string = "c") {
    console.log(a)
    console.log(b)
    console.log(c)
}
test2("x", "y")
```

* 可选参数：在方法的参数声明后面用问号来标明此参数为可选参数

```typescript
// 注意可选参数需要放置在必选参数后
function test(a:string, b?:string, c:string = "c") {
    console.log(a)
    console.log(b)
    console.log(c)
    console.log(b.length) // 需做处理
}
test("x")

function test2(a?:string, b:string, c:string = "c") {
    console.log(a)
    console.log(b)
    console.log(c)
}
test2("x")
```

### 3.3 函数新特性

* Rest and Spread操作符：用来声明任意数量的方法参数

```typescript
function fun1(...args) {
    args.forEach(function(arg) {
      console.log(arg)
    })
}

fun1(1, 2, 3)
fun1(5, 6, 7, 8, 9)
```

> typescript暂不支持的ES6语法

```typescript
function fun1(a, b, c) {
    console.log(a)
    console.log(b)
    console.log(c)
}

var args = [1, 2]
fun1(...args)

var args2 = [4, 5, 6, 7, 8]
fun1(...args2)
```

* generator函数：控制函数的执行过程，手工暂停和恢复代码执行

```typescript
function* doSomething() {
    console.log('start')
    
    yield
    
    console.log('end')
}

var func1 = doSomething()

func1.next()
func1.next()
```

```typescript
function* gerStockPrice() {
    while (true) {
        yield Math.random()*100
    }
}

var priceGenerator = gerStockPrice('IBM')

var limitPrice = 15

var price = 100

while (price > limitPrice){
    price = priceGenerator.next().value
    console.log(`the generator return ${price}`)
}

console.log(`buying at ${price}`)
```

* destructuring析构表达式：通过表达式将对象或数组拆解成任意数量的变量

从对象中取值

> ES5

```javascript
function getStock() {
    return {
        code: 'IBM',
        price: 100
    }
}
var stock = getStock()
var code = stock.code
var price = stock.price
```

> ES6

```typescript
function getStock() {
    return {
        code: 'IBM',
        price: 100
    }
}
var {code, price} = getStock()
console.log(code)
console.log(price)
// var {codex, price} = getStock()
// var {code: codex, price} = getStock()
// console.log(codex)
```

```typescript
function getStock() {
    return {
        code: 'IBM',
        price: {
            price1: 200,
            price2: 400
        },
        other: 'xxx'
    }
}
var {code, price} = getStock()
console.log(code)
console.log(price)
var {code, price: {price2}} = getStock()
console.log(code)
console.log(price)
```

从数组中取值

```typescript
var array1 = [1, 2, 3, 4]
var [number1, number2] = array1

console.log(number1)
console.log(number2)

var [,,number3, number4] = array1

console.log(number3)
console.log(number4)

var [number1,,, number4] = array1

console.log(number1)
console.log(number4)
```

```typescript
var array1 = [1, 2, 3, 4]
var [number1, number2, ...others] = array1

console.log(number1)
console.log(number2)
console.log(others)

function doSomething([number1, number2, ...others]) {
    console.log(number1)
    console.log(number2)
    console.log(others)
}
doSomething(array1)
```

## 参考资料

* [TypeScript 教程](https://www.runoob.com/typescript/ts-tutorial.html)
* [vue + typescript 新项目起手式](https://segmentfault.com/a/1190000011744210?utm_source=tuicool&utm_medium=referral)
