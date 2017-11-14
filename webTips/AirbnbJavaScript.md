# AirbnbJavaScript风格指南

#### 作者：高天阳

#### 邮箱：13683265113@163.com

```
更改历史

* 2017-11-14    高天阳    初始化文档
```

## 1 目录

1. 类型
1. 对象
1. 数组
1. 字符串
1. 函数
1. 属性
1. 变量
1. 提升
1. 比较运算符和等号
1. 块
1. 注释
1. 空白
1. 逗号
1. 分号
1. 类型转化
1. 命名规则
1. 存取器
1. 构造函数
1. 事件
1. 模块
1. jQuery的
1. ECMAScript 5兼容性
1. 测试
1. 性能
1. 资源
1. 谁在使用
1. 翻译
1. JavaScript风格指南说明
1. 与我们讨论JavaScript
1. 贡献者
1. 许可

## 2 正文

### 2.1 类型

- **原始值**：存取直接作用于它自身。
    - string
    - number
    - boolean
    - null
    - undefined
    
```angular2html
var foo = 1;
var bar = foo;

bar = 9;

console.log(foo, bar); // => 1, 9
```

- **复杂类型**：存在时作用于它自身值的引用。
    - object
    - array
    - function
    
```angular2html
var foo = [1, 2];
var bar = foo;

bar[0] = 9;

console.log(foo[0], bar[0]); // => 9, 9
```

### 2.2 对象

- 使用直接量创建对象。

```angular2html
// bad
var item = new Object();

// good
var item = {};
```

- 不要使用[保留字](http://es5.github.io/#x7.6.1)作为键名，它们在IE8下不工作。[更多信息](https://github.com/airbnb/javascript/issues/61)。

```angular2html
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

```angular2html
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

### 2.3 数组

- 使用直接量创建数组。

```angular2html
// bad
var items = new Array();

// good
var items = [];
```

- 向数组增加元素时使用Array＃push来替代直接赋值。

javascript 

var someStack = [];

```angular2html
// bad
someStack[someStack.length] = 'abracadabra';

// good
someStack.push('abracadabra');
```

- 当你需要拷贝数组时，使用Array＃[slice。jsPerf](https://jsperf.com/converting-arguments-to-an-array/7)

```angular2html
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

```angular2html
// bad
var a = [1,2,3];
var b = a;

console.log(a);// => [1,2,3]
console.log(b);// => [1,2,3]

a[0]=4;

console.log(a);// => [4,2,3]
console.log(b);// => [4,2,3]
```

```angular2html
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

```angular2html
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

```angular2html
function trigger() {
  var args = Array.prototype.slice.call(arguments);
  ...
}
```

> Demo

```angular2html
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

### 2.4 字符串

- 

```angular2html

```

- 

```angular2html

```

- 



> 难点：最佳实践，超出于示例，应该归纳总结出积累的技巧。

## 3 同类技术对比

> 难点：归纳比对项

## 参考资料

* [大道至简非简博客](http://www.jianshu.com/p/86331bdbf970)