# ES6新特性

#### 作者：王志伟
#### 邮箱：wangzhiwei@yumaomoney.com

```
更改历史

* 2018-11-20        高天阳     模板字符串、对象扩展、默认参数、import 和 export
* 2018-11-20        高天阳     整理文档
* 2018-11-13        王志伟     初始化文档

```

## 1 简介

ES6是前端开发的主力语言 （Vue、 React）如果你不能熟练掌握 需要补习~

## 2 使用

> ES6主要新特性

1. Default Parameters（默认参数） in ES6
1. Template Literals （模板文本）in ES6
1. Multi-line Strings （多行字符串）in ES6
1. Destructuring Assignment （解构赋值）in ES6
1. Enhanced Object Literals （增强的对象文本）in ES6
1. Arrow Functions （箭头函数）in ES6
1. Promises in ES6
1. Block-Scoped Constructs Let and Const（块作用域构造Let and Const）
1. Classes（类） in ES6
1. Modules（模块） in ES6

### 2.1 默认参数
### 2.2 模板文本

在其它语言中，使用模板和插入值是在字符串里面输出变量的一种方式。因此，在ES5，我们可以这样组合一个字符串：

```javascript
var name = 'Your name is ' + first + ' ' + last + '.';
var url = 'http://localhost:3000/api/messages/' + id;
```
幸运的是，在ES6中，我们可以使用新的语法$ {NAME}，并把它放在反引号里：

```javascript
var name = `Your name is ${first} ${last}. `;
var url = `http://localhost:3000/api/messages/${id}`;
```

### 2.3 多行字符串

```javascript
// ES6的多行字符串是一个非常实用的功能。在ES5中，我们不得不使用以下方法来表示多行字符串：

var roadPoem = 'Then took the other, as just as fair,nt'
   + 'And having perhaps the better claimnt'
   + 'Because it was grassy and wanted wear,nt'
   + 'Though as for that the passing therent'
   + 'Had worn them really about the same,nt';
var fourAgreements = 'You have the right to be you.n
   You can only be you when you do your best.';
   
// 然而在ES6中，仅仅用反引号就可以解决了：

var roadPoem = `Then took the other, as just as fair,
   And having perhaps the better claim
   Because it was grassy and wanted wear,
   Though as for that the passing there
   Had worn them really about the same,`;
var fourAgreements = `You have the right to be you.
   You can only be you when you do your best.`;
```

### 2.4 解构赋值

ES6 允许按照一定模式，从数组和对象中提取值，对变量进行赋值，这被称为解构（Destructuring）。
本质上，这种写法属于“模式匹配”，只要等号两边的模式相同，左边的变量就会被赋予对应的值。下面是一些使用嵌套数组进行解构的例子

```javascript
// 以前
let a = 1;
let b = 2;
let c = 3;

// 现在
let [a, b, c] = [1, 2, 3];

let [foo, [[bar], baz]] = [1, [[2], 3]];
foo //
bar //
baz //
let [ , , third] = ["foo", "bar", "baz"];
third //
let [x, , y] = [1, 2, 3];
x //
y //
let [head, ...tail] = [1, 2, 3, 4];
head //
tail //
let [x, y, ...z] = ['a'];
x //
y //
z //
```

如果解构不成功，变量的值就等于undefined

```javascript
let [foo] = [];
let [bar, foo] = [1];
```
另一种情况是不完全解构，即等号左边的模式，只匹配一部分的等号右边的数组。这种情况下，解构依然可以成功。

```javascript
let [x, y] = [1, 2, 3];
x //
y //
let [a, [b], d] = [1, [2, 3], 4];
a //
b //
d //
```

如果等号的右边不是数组（或者严格地说，不是可遍历的结构，参见《Iterator》一章），那么将会报错。

```javascript
let [foo] = 1;
let [foo] = false;
let [foo] = NaN;
let [foo] = undefined;
let [foo] = null;
let [foo] = {};
```

### 2.5 增强的对象文本
### 2.6 箭头函数

```javascript
    //ES5
    var evens = [1,3,5,7];
    var odds = evens.map(function(val){
        return val + 1
    })
    console.log(odds)
    //ES6
    var evens = [1,3,5,7];
    var odds = evens.map(v => v + 1)
    console.log(odds)
```

### 2.7 Promise构造函数
### 2.8 块作用域构造Let and Const

#### 2.8.1 Let 命令

用来声明变量。它的用法类似于var ，但是所声明的变量，只在let 命令所在的代码块内有效。

```javascript
 {
    let a = 123
    var b =456
  }
  console.log(a) //
  console.log(b) //
  // 不存在变量提升
  console.log(foo); //
  var foo = 2;

  console.log(bar); //
  let bar = 2;

```
变量i 是var 命令声明的，在全局范围内都有效，所以全局只有一个变量i
变量i 是let 声明的，当前的i 只在本轮循环有效，所以每一次循环的i 其实都是一个新的变量，

如果每一轮循环的变量i 都是重新声明的，那它怎么知道上一轮循环的值，从而计算出本轮循环的值？

```javascript
    //for 循环的计数器，就很合适使用let 命令
    var a = []
    for (let i = 0; i < 10; i++) {
        a[i] = function () {
            console.log(i);
            // 这里的i
        }
    }
    a[6]() // 10
    a[7]()

    console.log(i)// ? 10
    let i = 10 // 报错
```
答案：这是因为 JavaScript 引擎内部会记住上一轮循环的值，初始化本轮的变量i 时，就在上一轮循环的基础上进行计算

for 循环还有一个特别之处，就是设置循环变量的那部分是一个父作用域，而循环体内部是一个单独的子作用域。

```javascript
    for (let i = 0; i < 3; i++) {
        let i = 'abc';
        console.log(i);
    }

```

暂时性死区

```javascript
    var tmp = 123;
    if (true) {
        // TDZ开始
        tmp = 'abc'; // ReferenceError
        console.log(tmp); // ReferenceError
        let tmp; // TDZ结束
        console.log(tmp); // undefined
        tmp = 123;
        console.log(tmp); // 123
    }
```

答案：
上面代码中，存在全局变量tmp ，但是块级作用域内let 又声明了一个局部变量tmp ，导致后者绑定这个块级作用域，所以在let 声明变量前，对tmp 赋值会报错。
ES6 明确规定，如果区块中存在let 和const 命令，这个区块对这些命令声明的变量，从一开始就形成了封闭作用域。凡是在声明之前就使用这些变量，就会报错。

```javascript
    typeof x; // ReferenceError
    let x;
    typeof a // "undefined"
```

注意：养成良好的变成习惯，变量一定要在声明之后使用

```javascript
    function bar(x = y, y = 2) {
        return [x, y];
    }
    bar(); //
```

不允许重复声明

```javascript
    function func() {
        let a = 10;
        var a = 1; //
    }

    function func() {
        let a = 10;
        let a = 1; //
    }

    function func(arg) {
        let arg; //
    }

    function func(arg) {
        {
            let arg; //
        }
    }
```

#### 2.8.2 块作用域

内层变量可能会覆盖外层变量

```javascript
    var tmp = new Date();
    function f() {
        console.log(tmp);
        if (false) {
            var tmp = 'hello world';
        }
    }
    f(); //
```

用来计数的循环变量泄露为全局变量

```javascript
    var s = 'hello';
    for (var i = 0; i < s.length; i++) {
        console.log(s[i]);
    }
    console.log(i);
```
ES6 的块级作用域

```javascript
function f1() {
    let n = 5;
    if (true) {
        let n = 10;
    }
    console.log(n);
}
```

```javascript
    {{{{
        {let insane = 'Hello World'}
        console.log(insane); // 报错
    }}}};
```
块级作用域的出现，实际上使得获得广泛应用的立即执行函数表达式（IIFE）不再必要了

```javascript
// IIFE 写法(立即执行函数)
(function () {
    var tmp = ...; //此处是块级（私有）作用域
    ...
}());
// 块级作用域写法
{
    let tmp = ...;
    ...
}
```

#### 2.8.3 const

```javascript
    //ES5中的写法 大写
    Object.defineProperty(window,"PI2",{
        value: 3.1415926,
        writable: false
    })
    //ES6
    const PI = 3.1415926
    console.log(PI)
    PI = 4
```

声明一个只读的常量。一旦声明，常量的值就不能改变。

```javascript
    const PI = 3.1415;
    PI // 3.1415
    PI = 3;
    // TypeError: Assignment to constant variable.

    const foo //
```
const 声明的变量不得改变值，这意味着， const 一旦声明变量，就必须立即初始化，不能留到以后赋值。
同样存在暂时性死区 不可重复声明

```javascript
const a = [];
a.push('Hello'); //
a.length = 0; //
a = ['Dave']; //
```

对象冻结

```javascript
    const foo = Object.freeze({});
    // 常规模式时，下面一行不起作用；
    // 严格模式时，该行会报错
    foo.prop = 123;
```

### 2.9 类
### 2.10 模块
### 2.11 扩展运算符
### 2.12 顶层对象的属性

```javascript
    window.a = 1;
    a // 1
    a = 2;
    window.a // 2
```
上面代码中，顶层对象的属性赋值与全局变量的赋值，是同一件事。
顶层对象的属性与全局变量挂钩，被认为是 JavaScript 语言最大的设计败笔之一。这样的设计带来了几个很大的问题，首先是没法在编译时就报出变量未
声明的错误，只有运行时才能知道（因为全局变量可能是顶层对象的属性创造的，而属性的创造是动态的）；其次，程序员很容易不知不觉地就创建了全
局变量（比如打字出错）；最后，顶层对象的属性是到处可以读写的，这非常不利于模块化编程。另一方面， window 对象有实体含义，指的是浏览器的窗
口对象，顶层对象是一个有实体含义的对象，也是不合适的。
ES6 为了改变这一点，一方面规定，为了保持兼容性， var 命令和function 命令声明的全局变量，依旧是顶层对象的属性；另一方面规定， let 命令、
const 命令、class 命令声明的全局变量，不属于顶层对象的属性。也就是说，从 ES6 开始，全局变量将逐步与顶层对象的属性脱钩。

```javascript
    var a = 1;
    // 如果在 Node 的 REPL 环境，可以写成 global.a
    // 或者采用通用方法，写成 this.a
    window.a // 1
    let b = 1;
    window.b //
```

## 参考资料

* [ES6这些就够了](https://www.jianshu.com/p/287e0bb867ae)
* [es6的十大特性](https://www.jianshu.com/p/53fe8b56cfb0)
