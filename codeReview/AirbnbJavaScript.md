# AirbnbJavaScript风格指南

#### 作者：高天阳

#### 邮箱：13683265113@163.com

```
更改历史

* 2018-09-14    高天阳    更新目录
* 2017-11-14    高天阳    初始化文档
```

## 1 目录

1. [类型](#类型)
1. [对象](#对象)
1. [数组](#数组)
1. [字符串](#字符串)
1. [函数](#函数)
1. [属性](#属性)
1. [变量](#变量)
1. [提升](#提升)
1. [比较运算符和等号](#比较运算符和等号)
1. [块](#块)
1. [注释](#注释)
1. [空白](#空白)
1. [逗号](#逗号)
1. [分号](#分号)
1. [类型转化](#类型转化)
1. [命名规则](#命名规则)
1. [存取器](#存取器)
1. [构造函数](#构造函数)
1. [事件](#事件)
1. [模块](#模块)
1. [jQuery的](#jQuery的)
1. [ECMAScript 5兼容性](#ECMAScript 5兼容性)
1. [测试](#测试)
1. [性能](#性能)
1. [资源](#资源)
1. [谁在使用](#谁在使用)
1. [翻译](#翻译)
1. [JavaScript风格指南说明](#JavaScript风格指南说明)
1. [与我们讨论JavaScript](#与我们讨论JavaScript)
1. [贡献者](#贡献者)
1. [许可](#许可)

## 2 正文

### 2.1 类型{#类型}

- **原始值**：存取直接作用于它自身。
    - string
    - number
    - boolean
    - null
    - undefined
    
```
var foo = 1;
var bar = foo;

bar = 9;

console.log(foo, bar); // => 1, 9
```

- **复杂类型**：存在时作用于它自身值的引用。
    - object
    - array
    - function
    
```
var foo = [1, 2];
var bar = foo;

bar[0] = 9;

console.log(foo[0], bar[0]); // => 9, 9
```

### 2.2 对象{#对象}

- 使用直接量创建对象。

```
// bad
var item = new Object();

// good
var item = {};
```

- 不要使用[保留字](http://es5.github.io/#x7.6.1)作为键名，它们在IE8下不工作。[更多信息](https://github.com/airbnb/javascript/issues/61)。

```
// bad
var superman = {
  default: { clark: 'kent' },
  private: true
};

// good
var superman = {
  defaults: { clark: 'kent' },
  hidden: true
};
```

- 使用同义词替换需要使用的保留字。

```
// bad
var superman = {
  class: 'alien'
};

// bad
var superman = {
  klass: 'alien'
};

// good
var superman = {
  type: 'alien'
};
```

### 2.3 数组{#数组}

- 使用直接量创建数组。

```
// bad
var items = new Array();

// good
var items = [];
```

- 向数组增加元素时使用Array＃push来替代直接赋值。

javascript 

var someStack = [];

```
// bad
someStack[someStack.length] = 'abracadabra';

// good
someStack.push('abracadabra');
```

- 当你需要拷贝数组时，使用Array＃[slice。jsPerf](https://jsperf.com/converting-arguments-to-an-array/7)

```
var len = items.length;
var itemsCopy = [];
var i;

// bad
for (i = 0; i < len; i++) {
  itemsCopy[i] = items[i];
}

// good
itemsCopy = items.slice();
```

> Demo

```
// bad
var a = [1,2,3];
var b = a;

console.log(a);// => [1,2,3]
console.log(b);// => [1,2,3]

a[0]=4;

console.log(a);// => [4,2,3]
console.log(b);// => [4,2,3]
```

```
// bad
var a = [1,2,3];
var b = [];

console.log(a);// => [1,2,3]
console.log(b);// => []

for(var i=0; i<a.length; i++){b[i]=a[i]}

console.log(a);// => [1,2,3]
console.log(b);// => [1,2,3]

a[0]=4;

console.log(a);// => [4,2,3]
console.log(b);// => [1,2,3]
```

```
// good
var a = [1,2,3];
var b = a.slice();

console.log(a);// => [1,2,3]
console.log(b);// => [1,2,3]

a[0]=4;

console.log(a);// => [4,2,3]
console.log(b);// => [1,2,3]
```

- 使用[Array＃slice](https://www.cnblogs.com/dingxiaoyue/p/4948166.html)将类数组对象转换成数组。

```
function trigger() {
  var args = Array.prototype.slice.call(arguments);
  ...
}
```

> Demo

```
function trigger() {
  var args = Array.prototype.slice.call(arguments);
  return args
}
function trigger2() {
  return arguments
}

// bad
a = trigger2('a','b','c','d') // 此时a为类数组对象
a.push('e');// => Uncaught TypeError: a.push is not a function

// good
a = trigger('a','b','c','d') // 此时a为数组对象
a.push('e');
console.log(a);// => ["a", "b", "c", "d", "e"]
```

### 2.4 字符串{#字符串}

- 使用单引号''包裹字符串。

```
// bad
var name = "Bob Parr";

// good
var name = 'Bob Parr';

// bad
var fullName = "Bob " + this.lastName;

// good
var fullName = 'Bob ' + this.lastName;
```

- 超过100个字符的字符串应该使用连接符写成多行。

- 注：若过度使用，通过连接符连接的长字符串可能会影响性能。[jsPerf](https://jsperf.com/ya-string-concat)＆[讨论](https://github.com/airbnb/javascript/issues/40)。

```
// bad
var errorMessage = 'This is a super long error that was thrown because of Batman. When you stop to think about how Batman had anything to do with this, you would get nowhere fast.';

// bad
var errorMessage = 'This is a super long error that was thrown because \
of Batman. When you stop to think about how Batman had anything to do \
with this, you would get nowhere \
fast.';

// good
var errorMessage = 'This is a super long error that was thrown because ' +
  'of Batman. When you stop to think about how Batman had anything to do ' +
  'with this, you would get nowhere fast.';
```

- 程序化生成的字符串使用Array＃join连接而不是使用连接符。尤其是IE下：[jsPerf](http://jsperf.com/string-vs-array-concat/2)。

```
var items;
var messages;
var length;
var i;

messages = [{
  state: 'success',
  message: 'This one worked.'
}, {
  state: 'success',
  message: 'This one worked as well.'
}, {
  state: 'error',
  message: 'This one did not work.'
}];

length = messages.length;

// bad
function inbox(messages) {
  items = '<ul>';

  for (i = 0; i < length; i++) {
    items += '<li>' + messages[i].message + '</li>';
  }

  return items + '</ul>';
}

// good
function inbox(messages) {
  items = [];

  for (i = 0; i < length; i++) {
    // use direct assignment in this case because we're micro-optimizing.
    items[i] = '<li>' + messages[i].message + '</li>';
  }

  return '<ul>' + items.join('') + '</ul>';
}
```

### 2.5 函数{#函数}

- 函数表达式：

```
// 匿名函数表达式
var anonymous = function() {
  return true;
};

// 命名函数表达式
var named = function named() {
  return true;
};

// 立即调用的函数表达式（IIFE）
(function () {
  console.log('Welcome to the Internet. Please follow me.');
}());
```

- 永远不要在一个非函数代码块（if，while等）中声明一个函数，把那个函数赋予给一个变量。但是它们的解析表现不一致。

- **注意： ECMA-262**把`块`定义为一组语句。函数声明不是语句。[阅读对ECMA-262这个问题的说明](http://www.ecma-international.org/publications/files/ECMA-ST/Ecma-262.pdf#page=97)。

```
// bad
if (currentUser) {
  function test() {
    console.log('Nope.');
  }
}

// good
var test;
if (currentUser) {
  test = function test() {
    console.log('Yup.');
  };
}
```

- 永远不要把参数命名为`arguments`。将这取代函数作用英文域内的`arguments`对象。

```
// bad
function nope(name, options, arguments) {
  // ...stuff...
}

// good
function yup(name, options, args) {
  // ...stuff...
}
```

### 2.6 属性{#属性}

- 使用`.`来访问对象的属性。

```
var luke = {
  jedi: true,
  age: 28
};

// bad
var isJedi = luke['jedi'];

// good
var isJedi = luke.jedi;
```

- 当通过变量访问属性时使用中括号`[]`。

```
var luke = {
  jedi: true,
  age: 28
};

function getProp(prop) {
  return luke[prop];
}

var isJedi = getProp('jedi');
```

### 2.7 变量{#变量}

- 使用总是`var`来声明变量。不这么做将导致产生全局变量。我们要避免污染全局命名空间。

```
// bad
superPower = new SuperPower();

// good
var superPower = new SuperPower();
```
- 使用`var`声明每一个变量。

这样做的好处是增加新变量将变的更加容易，你而且永远不用再担心调换错`;`跟`,`。

```
// bad
var items = getItems(),
    goSportsTeam = true,
    dragonball = 'z';

// bad
// （跟上面的代码比较一下，看看哪里错了）
var items = getItems(),
    goSportsTeam = true;
    dragonball = 'z';

// good
var items = getItems();
var goSportsTeam = true;
var dragonball = 'z';
```
- 最后再声明未赋值的变量。当你需要引用前面的变量赋值时这将变的很有用。

```
// bad
var i, len, dragonball,
    items = getItems(),
    goSportsTeam = true;

// bad
var i;
var items = getItems();
var dragonball;
var goSportsTeam = true;
var len;

// good
var items = getItems();
var goSportsTeam = true;
var dragonball;
var length;
var i;
```
- 在作用域顶部声明变量。这将帮你避免变量声明提升相关的问题。

```
// bad
function () {
  test();
  console.log('doing stuff..');

  //..other stuff..

  var name = getName();

  if (name === 'test') {
    return false;
  }

  return name;
}

// good
function () {
  var name = getName();

  test();
  console.log('doing stuff..');

  //..other stuff..

  if (name === 'test') {
    return false;
  }

  return name;
}

// bad - 不必要的函数调用
function () {
  var name = getName();

  if (!arguments.length) {
    return false;
  }

  this.setFirstName(name);

  return true;
}

// good
function () {
  var name;

  if (!arguments.length) {
    return false;
  }

  name = getName();
  this.setFirstName(name);

  return true;
}
```
- 

```

```
- 

```

```



> 难点：最佳实践，超出于示例，应该归纳总结出积累的技巧。

## 3 同类技术对比

> 难点：归纳比对项

## 参考资料

* [大道至简非简博客](http://www.jianshu.com/p/86331bdbf970)