# ES6新特性

#### 作者：王志伟
#### 邮箱：wangzhiwei@yumaomoney.com

```
更改历史

* 2018-11-20        高天阳     默认参数、模板字符串、增强的对象字面量
* 2018-11-19        高天阳     整理文档
* 2018-11-13        王志伟     初始化文档

```

## 1 简介

ES6是前端开发的主力语言 （Vue、 React）如果你不能熟练掌握 需要补习~

## 2 使用

> ES6主要新特性

1. Functions （函数）in ES6
    1. Default Parameters（默认参数） in ES6
    1. Arrow Functions （箭头函数）in ES6
1. Strings （字符串）in ES6
    1. Template Literals （模板字符串）in ES6
    1. Multi-line Strings （多行字符串）in ES6
1. Destructuring Assignment （解构赋值）in ES6
1. Enhanced Object Literals （增强的对象字面量）in ES6
1. Promises in ES6
1. Block-Scoped Constructs Let and Const（块作用域构造Let and Const）
1. Classes（类） in ES6
1. Modules（模块） in ES6
1. Extension operators（扩展运算符） in ES6
1. Properties of top-level objects（顶层对象的属性） in ES6

### 2.1 函数

#### 2.1.1 默认参数

在ES5我们给函数定义参数默认值是怎么样？

```javascript
function action(num, color, url) {
    num = num || 200
    //当传入num时，num为传入的值
    //当没传入参数时，num即有了默认值200
    color = color || 'red';
    url = url || 'http://azat.co';
    return (num, color, url)
}
```

但细心观察的同学们肯定会发现，num传入为0的时候就是false，但是我们实际的需求就是要拿到num = 0，
此时num = 200 明显与我们的实际想要的效果明显不一样

ES6为参数提供了默认值。在定义函数时便初始化了这个参数，以便在参数没有被传递进去时使用。

```javascript
function action(num = 200) {
    console.log(num)
}
action(0)   //
action()    //
action(300) //
```

<!--
action(0)   //0
action()    //200
action(300) //300
-->

#### 2.1.2 箭头函数

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

#### 2.1.3 面试题

> 参数默认值的位置

通常情况下，定义了默认值的参数，应该是函数的尾参数。因为这样比较容易看出来，到底省略了哪些参数。如果非尾部的参数设置默认值，
实际上这个参数是没法省略的。

// 例一

```javascript
function f(x = 1, y) {
  return [x, y];
}
f()             //
f(2)            //
f(, 1)          //
f(undefined, 1) //
```

<!--
f()             // [1, undefined] 
f(2)            // [2, undefined]) 
f(, 1)          // 报错 
f(undefined, 1) // [1, 1]
-->

// 例二

```javascript
function f(x, y = 5, z) {
    return [x, y, z];
}
f()                 //
f(1)                //
f(1, ,2)            //
f(1, undefined, 2)  //
```

<!--
f()                 // [undefined, 5, undefined] 
f(1)                // [1, 5, undefined]
f(1, ,2)            // 报错
f(1, undefined, 2)  // [1, 5, 2]
-->

上面代码中，有默认值的参数都不是尾参数。这时，无法只省略该参数，而不省略它后面的参数，除非显式输入 undefined 。
 如果传入 undefined ，将触发该参数等于默认值， null 则没有这个效果。
 
```javascript
function foo(x = 5, y = 6) {
  console.log(x, y);
}
foo(undefined, null)
```

<!--
// 5 null
-->

上面代码中， x 参数对应 undefined ，结果触发了默认值， y 参数等于 null ，就没有触发默认值。

> 函数的 length 属性

```javascript
function calc(x=0, y=0) {
    // ...
    console.log(x, y)
}
function ajax(url, async = true, dataType = "JSON") {
    // ...
    console.log(url, async, dataType)
}
function foo(a, b, c = 5) {
    // ...
    console.log(a, b, c)
}
console.log(calc.length); //
console.log(ajax.length); //
console.log(foo.length);  //
```

<!--
console.log(calc.length); // 0
console.log(ajax.length); // 1
console.log(foo.length);  // 2
-->

定义了默认参数后，函数的length属性会减少，即有几个默认参数不包含在length的计算当中

```javascript
function foo (a = 0, b, c) {
    console.log(a, b, c)
}
function bar (a, b = 1, c) {
    console.log(a, b, c)
}
console.log(foo.length); //
console.log(bar.length); //
```

<!--
console.log(foo.length); // 0
console.log(bar.length); // 1
-->

如果设置了默认值的参数不是尾参数，那么 length 属性也不再计入后面的参数了。

```javascript
function ajax(url="../user.action", async=true, success) {
    var url = ''; //
    let async = 3; //
    const success = function(){}; //
}
```

<!--
var url = '';   // 允许
let async = 3;  // 报错
const success = function(){}; // 报错
-->

不能用let和const再次声明默认值，var可以

```javascript
function throwIf() {
    throw new Error('少传了参数');
}
 
function ajax(url=throwIf(), async=true, success) {
    return url;
}
ajax(); //
```

<!--
ajax(); // Error: 少传了参数
-->

可以看到这里参数success是一个函数调用，调用ajax时如果没有传第三个参数，
则会执行getCallback函数，该函数返回一个新函数赋值给success。
这是一个很强大的功能，给程序员以很大的想象发挥空间。

一旦设置了参数的默认值，函数进行声明初始化时，参数会形成一个单独的作用域(context)。
等到初始化结束，这个作用域就会消失。这种语法行为， 在不设置参数默认值时，是不会出现的。

```javascript
var x = 1;
function f(x, y = x) { 
    console.log(y);
}
f(2) //
```

<!--
f(2) // 2
-->

上面代码中，参数 y 的默认值等于变量 x 。调用函数 f 时，参数形成一个单独的作用域。
在这个作用域里面，默认值变量 x 指向第一个参数 x ，而不是全局变量x，所以输出是2。

再看下面的例子。

```javascript
let x = 1;
function f(y = x) { 
      let x = 2;
      console.log(y);
}
f() //
```

<!--
f() // 1
-->

上面代码中，函数 f 调用时，参数 y = x 形成一个单独的作用域。这个作用域里面，变量 x 本身没有定义，所以指向外层的全局变量 x 。
函数调用时，函数体内部的局部变量 x 影响不到默认值变量 x 。

```javascript
function bar(x = y, y = 2) {
    return [x, y];
}
bar();  //
```

<!--
报错(y is not defined) 2
-->

默认参数赋值会按照传入参数先后顺序进行，因此未定义就使用会报错

```javascript
var x = 1;
function foo(x = x) {
    // ...
}
foo();  //
```

<!--
报错(x is not defined)
-->

上面代码中，参数 x = x 形成一个单独作用域。实际执行的是 let x = x ，由于暂时性死区的原因，这行代码会报错”x 未定义“。

如果参数的默认值是一个函数，该函数的作用域也遵守这个规则。请看下面的例子。

```javascript
let foo = 'outer';
function bar(func = () => foo ) {
    let foo = 'inner'
    console.log(func());
}
bar();  //
```

<!--
bar();  // outer
-->

上面代码中，函数 bar 的参数 func 的默认值是一个匿名函数，返回值为变量 foo 。
函数参数形成的单独作用域里面，并没有定义变量 foo ，所以 foo 指向 外层的全局变量 foo ，因此输出 outer 。

如果写成下面这样，会如何呢。

```javascript
function bar(func = () => foo) {
    let foo = 'inner';
    console.log(func());
}
bar() //
```

<!--
bar();  // ReferenceError: foo is not defined
-->

上面代码中，匿名函数里面的 foo 指向函数外层，但是函数外层并没有声明变量 foo，所以就报错了。

下面是一个更复杂的例子。

```javascript
    var x = 1;
    function foo(x, y = function() { x = 2; }) {
        var x = 3;
        y(); console.log(x);
    }
    foo() //
    x     //
```

<!--
foo()   // 3
x       // 1
-->

上面代码中，函数 foo 的参数形成一个单独作用域。这个作用域里面，首先声明了变量 x ，然后声明了变量 y ， y 的默认值是一个匿名函数。
这个匿名函数内部的变量 x ，指向同一个作用域的第一个参数 x 。函数 foo 内部又声明了一个内部变量 x ，
该变量与第一个参数 x 由于不是同一个作用域，所以不是同一个变量，因此执行 y 后，内部变量 x 和外部全局变量 x 的值都没变。

```javascript
    var x = 1;
    function foo(x, y = function() { x = 2; }) {
        x = 3;
        y(); console.log(x);
    }
    foo() //
    x     //
```

<!--
foo()   // 2
x       // 1
-->

如果将 var x = 3 的 var 去除，函数 foo 的内部变量 x 就指向第一个参数 x ，与匿名函数内部的 x 是一致的，
所以最后输出的就是 2 ，而外层的全局变量 x 依然不受影响。

### 2.2 字符串

#### 2.2.1 模板字符串

基本的字符串格式化。将表达式嵌入字符串中进行拼接。用${}来界定。

```javascript
//ES5 
var name = 'Your name is ' + first + ' ' + last + '.';
var url = 'http://localhost:3000/api/messages/' + id;
//ES6
var name = `Your name is ${first} ${last}. `;
var url = `http://localhost:3000/api/messages/${id}`;

//ES5 
var name = 'lux'
console.log('hello' + name)
//ES6
const name = 'lux'
console.log(`hello ${name}`) //hello lux
```

#### 2.2.2 多行字符串

在ES5时我们通过反斜杠(\)来做多行字符串或者字符串一行行拼接。ES6反引号(``)直接搞定。

```javascript
// ES6的多行字符串是一个非常实用的功能。在ES5中，我们不得不使用以下方法来表示多行字符串：

var roadPoem = 'Then took the other, as just as fair,nt'
   + 'And having perhaps the better claimnt'
   + 'Because it was grassy and wanted wear,nt'
   + 'Though as for that the passing therent'
   + 'Had worn them really about the same,nt';
var fourAgreements = 'You have the right to be you.\
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

#### 2.2.3 字符串判断、处理

对于字符串 ES6+ 当然也提供了很多厉害也很有意思的方法 说几个常用的。

```javascript
// 1.includes：判断是否包含然后直接返回布尔值
const str = 'hahay'
console.log(str.includes('y')) // true

// 2.repeat: 获取字符串重复n次
const str = 'he'
console.log(str.repeat(3)) // 'hehehe'
//如果你带入小数, Math.floor(num) 来处理
// s.repeat(3.1) 或者 s.repeat(3.9) 都当做成 s.repeat(3) 来处理

// 3. startsWith 和 endsWith 判断是否以 给定文本 开始或者结束
const str =  'hello world!'
console.log(str.startsWith('hello')) // true
console.log(str.endsWith('!')) // true

// 4. padStart 和 padEnd 填充字符串，应用场景：时分秒
setInterval(() => {
    const now = new Date()
    const hours = now.getHours().toString()
    const minutes = now.getMinutes().toString()
    const seconds = now.getSeconds().toString()
    console.log(`${hours.padStart(2, 0)}:${minutes.padStart(2, 0)}:${seconds.padStart(2, 0)}`)
}, 1000)
```

#### 2.2.4 面试题

* 模拟一个模板字符串的实现。

```javascript
let address = '北京海淀区'
let name = 'lala'
let str = '${name}在${address}上班...'
// 模拟一个方法 myTemplate(str) 最终输出 'lala在北京海淀区上班...'
function myTemplate(str) {
    // try it
}
console.log(myTemplate(str)) // lala在北京海淀区上班...
```

参考链接:[面试题：模板字符串的执行问题？](http://bugshouji.com/shareweb/t542)、
[Javascript动态执行JS（new Function与eval比较）](https://www.cnblogs.com/EasonJim/p/6228027.html)

<!--
var str =  'return ' + '`'+str+'`'
let func = new Function('name','address', str);
return func(name,address)
-->

* 实现标签化模板(自定义模板规则)。

```javascript
const name = 'cc'
const gender = 'male'
const hobby = 'basketball'
// 实现tag最终输出 '姓名：**cc**，性别：**male**，爱好：**basketball**'
function tag(strings) {
    // do it
}
const str = tag`姓名：${name}，性别：${gender}，爱好：${hobby}`
console.log(str) // '姓名：**cc**，性别：**male**，爱好：**basketball**'
```

<!--
  //方案1
  let result = `${strings[0]}**${name}**${strings[1]}**${gender}**${strings[2]}**${hobby}**`
  
  //方案2
  let result = '';
  for (let i = 0; i < strings.length-1; i++) {
    result += strings[i];
    result += '**';
    if(i===0){
      result += name
    }else if(i===1){
      result += gender
    }else if(i===2){
      result += hobby
    }
    result += '**';
  }
  //加上最后一个普通字符串。
  result += strings[strings.length - 1];
  return result;
-->

### 2.3 解构赋值

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

### 2.4 增强的对象字面量

使用对象文本可以做许多让人意想不到的事情！通过ES6，我们可以把ES5中的JSON变得更加接近于一个类。

下面是一个典型ES5对象文本，里面有一些方法和属性：

```javascript
var serviceBase = {port: 3000, url: 'azat.co'},
    getAccounts = function(){return [1,2,3]};
var accountServiceES5 = {
    port: serviceBase.port,
    url: serviceBase.url,
    getAccounts: getAccounts,
    toString: function() {
        return JSON.stringify(this.valueOf());
    },
    getUrl: function() {return "http://" + this.url + ':' + this.port},
    valueOf_1_2_3: getAccounts()
}
```

如果我们想让它更有意思，我们可以用Object.create从serviceBase继承原型的方法：

```javascript
var serviceBase = {port: 3000, url: 'azat.co'},
    getAccounts = function(){return [1,2,3]};
var accountServiceES5ObjectCreate = Object.create(serviceBase)
var accountServiceES5ObjectCreate = {
  getAccounts: getAccounts,
  toString: function() {
    return JSON.stringify(this.valueOf());
  },
  getUrl: function() {return "http://" + this.url + ':' + this.port},
  valueOf_1_2_3: getAccounts()
}
```

```javascript
var serviceBase = {port: 3000, url: 'azat.co'},
    getAccounts = function(){return [1,2,3]};
var accountServiceES5ObjectCreate = Object.create(serviceBase,{
    getAccounts: {
        get: getAccounts
    },
    toString: {
        get: function() {
             return JSON.stringify(this.valueOf());
        }
    },
    getUrl: {
        get: function() {
          return "http://" + this.url + ':' + this.port
        }
    },
    valueOf_1_2_3: {
        value: getAccounts()
    }
})
console.log(accountServiceES5ObjectCreate)
```

我们知道，accountServiceES5ObjectCreate 和accountServiceES5 并不是完全一致的，
因为一个对象(accountServiceES5)在proto对象中将有下面这些属性：

![](../assets/Es6/ES6-proto.png)

为了方便举例，我们将考虑它们的相似处。所以在ES6的对象文本中，既可以直接分配getAccounts: getAccounts,
也可以只需用一个getAccounts，此外，我们在这里通过proto（并不是通过’proto’）设置属性，如下所示：

```javascript
var serviceBase = {port: 3000, url: 'azat.co'},
getAccounts = function(){return [1,2,3]};
var accountService = {
    __proto__: serviceBase,
    getAccounts,
    // 另外，我们可以调用super防范，以及使用动态key值(valueOf_1_2_3):
    toString() 
    {
      return JSON.stringify((super.valueOf()));
    },
    getUrl() 
    {return "http://" + this.url + ':' + this.port},
    [ 'valueOf_' + getAccounts().join('_') ]: getAccounts()
};
console.log(accountService)
```

![](../assets/Es6/ES6-accountService.png)

ES6对象文本是一个很大的进步对于旧版的对象文本来说。

### 2.5 Promise构造函数
### 2.6 块作用域构造Let and Const

#### 2.6.1 Let 命令

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

#### 2.6.2 块作用域

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

```
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

#### 2.6.3 const

```
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

```
    const PI = 3.1415;
    PI // 3.1415
    PI = 3;
    // TypeError: Assignment to constant variable.

    const foo //
```
const 声明的变量不得改变值，这意味着， const 一旦声明变量，就必须立即初始化，不能留到以后赋值。
同样存在暂时性死区 不可重复声明

```
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

### 2.7 类
### 2.8 模块
### 2.9 扩展运算符
### 2.10 顶层对象的属性

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
