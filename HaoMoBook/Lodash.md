# Lodash

#### 作者：高天阳
#### 邮箱：gty@haomo-studio.com

```
更改历史

* 2017-12-2 	高天阳      增加示例
* 2017-11-12	戈德斯文    增加类比内容，更改页面格式
* 2017-9-25	    张飞        更改图片路径
* 2017-9-1	    申海东      初始化文档

```
## 1. 历史、现状和发展

### 1.1 什么是lodash

lodash库是一个具有一致接口、模块化、高性能等特性的 JavaScript 工具库。
有多年开发经验的工程师，往往都会有自己的一套工具库，称为 utils、helpers 等等，
这套库一方面是自己的技术积累，另一方面也是对某项技术的扩展，领先于技术规范的制定和实现，
需要用的时候直接饮用就可以了，不用再重新编写一套函数方法。
Lodash 就是这样的一套工具库，它内部封装了诸多对字符串、数组、对象等常见数据类型的处理函数，
其中部分是目前 ECMAScript 尚未制定的规范，但同时被业界所认可的辅助函数。
目前每天使用 npm 安装 Lodash 的数量在百万级以上，这在一定程度上证明了其代码的健壮性，值得我们在项目中一试。

### 1.2 现状

目前lodash已经更新到了V4，2015年是大年 Lodash成为最依赖于 npm的软件包，通过了10亿次下载，其v3版本也被大量采用！
并且lodash已经开始对于和underscore合并的事宜进行讨论。

最新版本支持Chrome 54-55，Firefox 49-50，IE 11，Edge 14，Safari 9-10，Node.js 6-7和 PhantomJS 2.1.1。

### 1.3 ES6大行其道的今天lodash怎么发展

1. Lodash 提供了很多 es6 里面没有的功能，真的有需求的时候还是可以用的
2. Lodash 还提供了几乎所有浏览器的兼容，从现代浏览器来说很多兼容是多余的，带来了很多不必要的流量
3. 对于server 端、框架或是工具库开发而言，如果无法预测代码会跑在什么环境，有 lodash 能少考虑很多兼容的问题少做很多测试
4. 很多方法都提供了 path 以及一些很方便的参数，可以大幅度减少代码量

## 2. 安装和使用

### 2.1 安装

在HTML使用script标签引入：  
```
<script src="lodash.js"></script>
```
直接下载下来引入，或者使用cdn

使用npm：  
```
$ npm install -g lodash
$ npm install --save lodash
```

* node.js使用：

```angular2html
var _ = require('lodash');
```

### 2.2 使用
`import _ from 'lodash'`，lodash默认使用的符号是下划线`_`，类似于jQuery的`$`符号;

### 2.3 示例（参考版本lodash v4.16.1）

#### 2.3.1、浅克隆对象 `_.clone(value)`

创建一个 value 的浅拷贝。 注意: 这个方法参考自 structured clone algorithm 以及支持
arrays、array buffers、 booleans、 date objects、maps、 numbers， Object 对象, regexes, sets, strings, symbols, 
以及 typed arrays。 arguments对象的可枚举属性会拷贝为普通对象。 一些不可拷贝的对象，例如error objects、functions, DOM nodes, 
以及 WeakMaps 会返回空对象。

* 添加版本
    * 0.1.0
* 参数
    * value (*): 要拷贝的值
* 返回
    * (*): 返回拷贝后的值。

```angular2html
vm.objects = [{ 'a': 1 }, { 'b': 2 }];

vm.shallow = vm.objects;
$log.log(vm.shallow === vm.objects);
$log.log(vm.shallow[0] === vm.objects[0]);


vm.objects = [{ 'a': 1 }, { 'b': 2 }];

vm.shallow = _.clone(vm.objects);
$log.log(vm.shallow === vm.objects);
$log.log(vm.shallow[0] === vm.objects[0]);
```
#### 2.3.2、深克隆对象 `_.cloneDeep(value)`

深度克隆JavaScript对象是困难的，并且也没有什么简单的解决方案。
你可以使用原生的解决方案:JSON.parse(JSON.stringify(objectToClone)) 进行深度克隆。
但是，这种方案仅在对象内部没有方法的时候才可行。

* 添加版本
    * 1.0.0
* 参数
    * value (*): 要深拷贝的值。
* 返回
    * (*): 返回拷贝后的值。

```angular2html
vm.objects = [{ 'a': 1 }, { 'b': 2 }];

vm.shallow = _.cloneDeep(vm.objects);
$log.log(vm.shallow === vm.objects);
$log.log(vm.shallow[0] === vm.objects[0]);
```

#### 2.3.3、遍历循环`_.forEach(collection, [iteratee=_.identity])`

这两种方法都会分别输出‘1’和‘2’，不仅是数组，对象也可以，数组的是后key是元素的下标，当传入的是对象的时候，key是属性，value是值

注意: 与其他"集合"方法一样，类似于数组，对象的 "length" 属性也会被遍历。想避免这种情况，可以用 `_.forIn` 或者 `_.forOwn` 代替。

效果和for循环的continue一致；

* 添加版本
    * 0.1.0
* 别名
    * _.each
* 参数
    * collection (Array|Object): 一个用来迭代的集合。
    * `[iteratee=_.identity]` (Function): 每次迭代调用的函数。
* 返回
    * (*): 返回集合 collection。

```angular2html
_([1, 2]).forEach(function(value) {
  $log.log(value);
});
_.forEach([1, 3] , function(value, key) {
  $log.log(value,key);
});
vm.users = [
    { 'user': 'barney',  'age': 36, 'active': true },
    { 'user': 'fred',    'age': 40, 'active': false },
    { 'user': 'pebbles', 'age': 1,  'active': true }
  ];
_.forEach(vm.users , function(v, k) {
  $log.log(v,k);
  v.age=1;
  $log.log(v,k);
});
```
#### 2.3.4、遍历循环执行某个方法 深层查找属性值`_.map(collection, [iteratee=_.identity])`

创建一个数组， value（值） 是 iteratee（迭代函数）遍历 collection（集合）中的每个元素后返回的结果。 iteratee（迭代函数）调用3个参数： 
(value, index|key, collection). 

Lodash中的_.map方法和JavaScript中原生的数组方法非常的像，但它还是有非常有用的升级。 
你可以通过一个字符串而不是回调函数来浏览深度嵌套的对象属性。

lodash 中有许多方法是防止作为其他方法的迭代函数（愚人码头注：即不能作为iteratee参数传递给其他方法），
例如： _.every, _.filter, _.map, _.mapValues, _.reject, 和 _.some。 

受保护的方法有（愚人码头注：即这些方法不能使用_.every, _.filter, _.map, _.mapValues, _.reject,
和 _.some作为 iteratee 迭代函数参数） ：
ary, chunk, curry, curryRight, drop, dropRight, every, fill, invert, parseInt, random, range, 
rangeRight, repeat, sampleSize, slice, some, sortBy, split, take, takeRight, template, trim,
 trimEnd, trimStart, and words

* 添加版本
    * 0.1.0
* 参数
    * collection (Array|Object): 用来迭代的集合。
    * [iteratee=_.identity] (Array|Function|Object|string): 每次迭代调用的函数。
* 返回
    * (Array): 返回新的映射后数组。

```angular2html
vm.users = [
  { 'user': 'barney',  'age': 36, 'active': true },
  { 'user': 'fred',    'age': 40, 'active': false },
  { 'user': 'pebbles', 'age': 1,  'active': true }
];

vm.test = _.map(vm.users , function(v) {
  v.user = v.user+'1';
  return v
});
$log.log(vm.test);

vm.users = [
  { 'user': 'barney',  'age': 36, 'active': true },
  { 'user': 'fred',    'age': 40, 'active': false },
  { 'user': 'pebbles', 'age': 1,  'active': true }
];

vm.test2 = _.each(vm.users , function(v) {
  return v.user == 'barney'
});
$log.log(vm.test2);
```

```angular2html
<script type="text/javascript">
   function square(n) {
       return n * n;
   }

   console.log(_.map([4, 8], square));
   // => [16, 64]

   console.log(_.map({ 'a': 4, 'b': 8 }, square));
   // => [16, 64] (iteration order is not guaranteed)

   var users = [
       { 'user': 'barney' },
       { 'user': 'fred' }
   ];

   // The `_.property` iteratee shorthand.
   console.log(_.map(users, 'user'));
   // => ['barney', 'fred']
</script>
```

#### 2.3.5、查找属性 `_.find(collection, [predicate=_.identity], [fromIndex=0])`

遍历 collection（集合）元素，返回 predicate（断言函数）第一个返回真值的第一个元素。
predicate（断言函数）调用3个参数： (value, index|key, collection)。

* 添加版本
    * 0.1.0
* 参数
    * collection (Array|Object): 一个用来迭代的集合。
    * `[predicate=_.identity]` (Array|Function|Object|string): 每次迭代调用的函数。
    * `[fromIndex=0]` (number): 开始搜索的索引位置。
* 返回
    * (*): 返回匹配元素，否则返回 undefined。
    
```
var users = [
  { 'user': 'barney',  'age': 36, 'active': true },
  { 'user': 'fred',    'age': 40, 'active': false },
  { 'user': 'pebbles', 'age': 1,  'active': true }
];
 
_.find(users, function(o) { return o.age < 40; });
// => object for 'barney'
 
// The `_.matches` iteratee shorthand.
_.find(users, { 'age': 1, 'active': true });
// => object for 'pebbles'
 
// The `_.matchesProperty` iteratee shorthand.
_.find(users, ['active', false]);
// => object for 'fred'
 
// The `_.property` iteratee shorthand.
_.find(users, 'active');
// => object for 'barney'
```

#### 2.3.6、查找属性 `_.filter(collection, [predicate=_.identity])`

遍历 collection（集合）元素，返回 predicate（断言函数）返回真值 的所有元素的数组。
predicate（断言函数）调用三个参数：(value, index|key, collection)。 

* 添加版本
    * 0.1.0
* 参数
    * collection (Array|Object): 一个用来迭代的集合。
    * `[predicate=_.identity]` (Array|Function|Object|string): 每次迭代调用的函数。
* 返回
    * (Array): 返回一个新的过滤后的数组。

```
var users = [
  { 'user': 'barney', 'age': 36, 'active': true },
  { 'user': 'fred',   'age': 40, 'active': false }
];
 
_.filter(users, function(o) { return !o.active; });
// => objects for ['fred']
 
// The `_.matches` iteratee shorthand.
_.filter(users, { 'age': 36, 'active': true });
// => objects for ['barney']
 
// The `_.matchesProperty` iteratee shorthand.
_.filter(users, ['active', false]);
// => objects for ['fred']
 
// The `_.property` iteratee shorthand.
_.filter(users, 'active');
// => objects for ['barney']
```

#### 2.3.7、查找属性 `_.reject(collection, [predicate=_.identity])`

`_.filter`的反向方法;此方法 返回 predicate（断言函数） 不 返回 truthy（真值）的collection（集合）元素（愚人码头注释：非真）。

* 添加版本
    * 0.1.0
* 参数
    * collection (Array|Object): 用来迭代的集合。
    * `[predicate=_.identity]` (Array|Function|Object|string): 每次迭代调用的函数。
* 返回
    * (Array): 返回过滤后的新数组
    
```
var users = [
  { 'user': 'barney', 'age': 36, 'active': false },
  { 'user': 'fred',   'age': 40, 'active': true }
];
 
_.reject(users, function(o) { return !o.active; });
// => objects for ['fred']
 
// `_.matches` 迭代简写
_.reject(users, { 'age': 40, 'active': true });
// => objects for ['barney']
 
// `_.matchesProperty` 迭代简写
_.reject(users, ['active', false]);
// => objects for ['fred']
 
// `_.property` 迭代简写
_.reject(users, 'active');
// => objects for ['barney']
```

#### 2.3.8、查找属性`_.find`与`_.filter`的比较

`_.find()`第一个返回真值的第一个元素。
`_.filter()`返回真值的所有元素的数组。
`_.reject()`是`_.filter()`的反向方法，不返回真值的（集合）元素

```angular2html
<script type="text/javascript">
    var users = [
        {'user': 'barney', 'age': 36, 'active': true},
        {'user': 'fred', 'age': 40, 'active': false},
        {'user': 'pebbles', 'age': 1, 'active': true}
    ];

    console.log(_.find(users, function (o) {
        return o.age < 40;
    }));
    console.log(_.find(users, {'age': 1, 'active': true}));
    console.log(_.filter(users, {'age': 1, 'active': true}));
    console.log(_.find(users, ['active', false]));
    console.log(_.filter(users, ['active', false]));
    console.log(_.find(users, 'active'));
    console.log(_.filter(users, 'active'));

</script>
```

#### 2.3.9、数组通过值去重 `_.uniq(array)`

创建一个去重后的array数组副本。使用了 SameValueZero 做等值比较。只有第一次出现的元素才会被保留。

* 添加版本
    * 0.1.0
* 参数
    * array (Array): 要检查的数组。
* 返回
    * (Array): 返回新的去重后的数组。

```angular2html
<script type="text/javascript">
    var arr1 = [2, 1, 2];

    var arr2 = _.uniq(arr1);


    function unique(arr) {
        var newArr = [];
        for (var i = 0; i < arr.length; i++) {
            if(newArr.indexOf(arr[i]) == -1){
                newArr.push(arr[i]);
            }
        }
        return newArr;
    }

    console.log(arr1);
    console.log(arr2);
    console.log(unique(arr1));
</script>
```

#### 2.3.10、数组通过方法去重 `_.uniqBy(array, [iteratee=_.identity])`

这个方法类似 `_.uniq` ，除了它接受一个 iteratee （迭代函数），调用每一个数组（array）的每个元素以产生唯一性计算的标准。
iteratee 调用时会传入一个参数：(value)。

* 添加版本
    * 4.0.0
* 参数
    * array (Array): 要检查的数组。
    * `[iteratee=_.identity]` (Array|Function|Object|string): 迭代函数，调用每个元素。
* 返回
    * (Array): 返回新的去重后的数组。

```angular2html
_.uniqBy([2.1, 1.2, 2.3], Math.floor);
// => [2.1, 1.2]
 
// The `_.property` iteratee shorthand.
_.uniqBy([{ 'x': 1 }, { 'x': 2 }, { 'x': 1 }], 'x');
// => [{ 'x': 1 }, { 'x': 2 }]
```
Math.floor只是向下取整，去重，并没有改变原有的数组，所以还是2.1和1.2，不是2和1。

#### 2.3.11、过滤返回新数组 `_.difference(array, [values])`

创建一个具有唯一array值的数组，每个值不包含在其他给定的数组中。
（愚人码头注：即创建一个新数组，这个数组中的值，为第一个数字（array 参数）排除了给定数组中的值。）
该方法使用 SameValueZero做相等比较。结果值的顺序是由第一个数组中的顺序确定。 

注意: 不像 `_.pullAll`，这个方法会返回一个新数组。

* 引入版本
    * 0.1.0
* 参数
    * array (Array): 要检查的数组。
    * `[values]` (...Array): 排除的值。
* 返回
    * (Array): 返回一个过滤值后的新数组。

```angular2html
_.difference([3, 2, 1], [4, 2]);
// => [3, 1]
```

#### 2.3.12、值过滤返回原数组 `_.pull(array, [values])`

* 参数
    * array (Array): 要修改的数组。
    * [values] (...*): 要删除的值。
* 返回值
    * (Array): 返回 array.

```angular2html
var array = [1, 2, 3, 1, 2, 3];
 
_.pull(array, 2, 3);
console.log(array);
// => [1, 1]
```

移除数组array中所有和给定值相等的元素，使用 SameValueZero 进行全等比较。 

注意：和 `_.without 方法不同`，这个方法会改变数组。使用 `_.remove` 从一个数组中移除元素。

#### 2.3.13、方法过滤返回新数组 `_.remove(array, [predicate=_.identity])`

去除符合条件的数组子项，改变原数组，返回被移除的子项组成的新数组

* 参数
    * array (Array): 要修改的数组。
    * [predicate=_.identity] (Array|Function|Object|string): 每次迭代调用的函数。
* 返回
    * (Array): 返回移除元素组成的新数组。

```angular2html
var array = [1, 2, 3, 4];
var evens = _.remove(array, function(n) {
  return n % 2 == 0;
});
 
console.log(array);
// => [1, 3]
 
console.log(evens);
// => [2, 4]
```

#### 2.3.14、替换`_.fill(array, value, [start=0], [end=array.length])`

使用 value 值来填充（替换） array，从start位置开始, 到end位置结束（但不包含end位置）。

Note: 这个方法会改变 array（愚人码头注：不是创建新数组）。

* 引入版本
    * 3.2.0
* 参数
    * array (Array): 要填充改变的数组。
    * value (*): 填充给 array 的值。
    * [start=0] (number): 开始位置（默认0）。
    * [end=array.length] (number):结束位置（默认array.length）。
* 返回值
    * (Array): 返回 array。

```
var array = [1, 2, 3];
 
_.fill(array, 'a');
console.log(array);
// => ['a', 'a', 'a']
 
_.fill(Array(3), 2);
// => [2, 2, 2]
 
_.fill([4, 6, 8, 10], '*', 1, 3);
// => [4, '*', '*', 10]
```

#### 2.3.15、剪裁数组 `_.slice(array, [start=0], [end=array.length])`

裁剪数组array，从 start 位置开始到end结束，但不包括 end 本身的位置。 

Note: 这个方法用于代替 Array#slice 来确保数组正确返回。

* 添加版本
    * 3.0.0
* 参数
    * array (Array): 要裁剪数组。
    * [start=0] (number): 开始位置。
    * [end=array.length] (number): 结束位置。
* 返回
    * (Array): 返回 数组array 裁剪部分的新数组。
    
```
var array = [1, 2, 3, 4, 5];
 
_.slice(array, 1, 3);
console.log(array);
```

#### 2.3.16、N次循环 `_.times(n, [iteratee=_.identity])`

调用 iteratee n 次，每次调用返回的结果存入到数组中。 iteratee 调用入1个参数： (index)。

for语句是执行循环的不二选择，但在上面代码的使用场景下，_.times()的解决方式更加简洁和易于理解。

相对于for循环，lodash提供了更为高效的循环方法：_.times(number,function); 该方法会返回一个数组；

* 添加版本
    * 0.1.0
* 参数
    * n (number): 调用 iteratee 的次数。
    * [iteratee=_.identity] (Function): 每次迭代调用的函数。
* 返回
    * (Array): 返回调用结果的数组。

```angular2html
<script type="text/javascript">
console.log('------- javascript -------');
//js原生的循环方法
for(var i = 0; i < 5; i++){
    console.log(i);
}
console.log('------- lodash -------');
//ladash的times方法
_.times(5,function(a){
    console.log(a);
});

_.times(3, String);
// => ['0', '1', '2']
 
 _.times(4, _.constant(0));
// => [0, 0, 0, 0]
</script>
```

```angular2html
 var i = 0;
 var time1 = _.times(3, function(){
     console.log(i++);
     return i;
 });
```
> 输出结果为：0, 1, 2

```angular2html
 var time2 = _.times(4, _.constant(0));
 console.log(time1, time2);

```
> 输出结果为： [1, 2, 3]    [0, 0, 0, 0]

使用_.times方法创建一个有相同前缀的值的数组；
```angular2html
 var newArr = _.times(6, _.partial(_.uniqueId, 'time_'));
 console.log(newArr);

```
> ["team_1", "team_2", "team_3", "team_4", "team_5", "team_6"];

#### 2.3.17、扩展对象`_.assign(object, [sources])`

分配来源对象的可枚举属性到目标对象上。 来源对象的应用规则是从左到右，随后的下一个对象的属性会覆盖上一个对象的属性。 

注意: 这方法会改变 object，参考自 Object.assign.

_.assign 方法也可以接收多个参数对象进行扩展，都是往后面的对象上合并

* 添加版本
    * 0.10.0
* 参数
    * object (Object): 目标对象。
    * [sources] (...Object): 来源对象。
* 返回
    * (Object): 返回 object.

```angular2html
<script type="text/javascript">
Object.prototype.extend = function(obj) {
    for (var i in obj) {
        if (obj.hasOwnProperty(i)) {    //判断被扩展的对象有没有某个属性，
            this[i] = obj[i];
        }
    }
};

var objA = {"name": "张三", "car": "宝马"};
var objB = {"name": "李四", "loveEat": true};

objA.extend(objB);
console.log(objA); 

console.log(_.assign(objA, objB));
</script>
```

#### 2.3.18、在指定范围内获取一个随机值 `_.random([lower=0], [upper=1], [floating])`

产生一个包括 lower 与 upper 之间的数。 如果只提供一个参数返回一个0到提供数之间的数。 
如果 floating 设为 true，或者 lower 或 upper 是浮点数，结果返回浮点数。 

注意: JavaScript 遵循 IEEE-754 标准处理无法预料的浮点数结果。

Lodash中的 _.random 方法要比上面的原生方法更强大与灵活。你可以只传入一个参数作为最大值， 
你也可以指定返回的结果为浮点数_.random(15,20,true)

* 添加版本
    * 0.7.0
* 参数
    * [lower=0] (number): 下限。
    * [upper=1] (number): 上限。
    * [floating] (boolean): 指定是否返回浮点数。
* 返回
    * (number): 返回随机数。

```angular2html
<script type="text/javascript">
_.random(0, 5);
// => an integer between 0 and 5
 
_.random(5);
// => also an integer between 0 and 5
 
_.random(5, true);
// => a floating-point number between 0 and 5
 
_.random(1.2, 5.2);
// => a floating-point number between 1.2 and 5.2

function getRandomNumber(min, max){
    return Math.floor(Math.random() * (max - min)) + min;
}
console.log(getRandomNumber(15, 20));

console.log(_.random(15, 20));

</script>
```

#### 2.3.19、查找元素索引值 `_.findIndex(array, [predicate=_.identity], [fromIndex=0])`

该方法类似_.find，区别是该方法返回第一个通过 predicate 判断为真值的元素的索引值（index），而不是元素本身。

* 引入版本
    * 1.1.0
* 参数
    * array (Array): 要搜索的数组。
    * [predicate=_.identity] (Array|Function|Object|string): 这个函数会在每一次迭代调用。
    * [fromIndex=0] (number): The index to search from.
* 返回值
    * (number): 返回找到元素的 索引值（index），否则返回 -1。
    
```
var users = [
  { 'user': 'barney',  'active': false },
  { 'user': 'fred',    'active': false },
  { 'user': 'pebbles', 'active': true }
];
 
_.findIndex(users, function(o) { return o.user == 'barney'; });
// => 0
 
// The `_.matches` iteratee shorthand.
_.findIndex(users, { 'user': 'fred', 'active': false });
// => 1
 
// The `_.matchesProperty` iteratee shorthand.
_.findIndex(users, ['active', false]);
// => 0
 
// The `_.property` iteratee shorthand.
_.findIndex(users, 'active');
// => 2
```

#### 2.3.20、获取数组第一个元素 `_.head(array)`

获取数组 array 的第一个元素。

* 引入版本
    * 0.1.0
* 别名
    * _.first
* 参数
    * array (Array): 要查询的数组。
* 返回值
    * (*): 返回数组 array的第一个元素。
    
```
_.head([1, 2, 3]);
// => 1
 
_.head([]);
// => undefined
```

#### 2.3.21、从列表中随机的选择列表项 `_.indexOf(array, value, [fromIndex=0])`

使用 SameValueZero 等值比较，返回首次 value 在数组array中被找到的 索引值， 如果 fromIndex 为负值，将从数组array尾端索引进行匹配。

* 引入版本
    * 0.1.0
* 参数
    * array (Array): 需要查找的数组。
    * value (*): 需要查找的值。
    * [fromIndex=0] (number): 开始查询的位置。
* 返回值
    * (number): 返回 值value在数组中的索引位置, 没有找到为返回-1。
    
```
_.indexOf([1, 2, 1, 2], 2);
// => 1
 
// Search from the `fromIndex`.
_.indexOf([1, 2, 1, 2], 2, 2);
// => 3
```

#### 2.3.22、从列表中随机的选择列表项 `_.sample(collection)`

从collection（集合）中获得一个随机元素。

* 添加版本
    * 2.0.0
* 参数
    * collection (Array|Object): 要取样的集合。
* 返回
    (*): 返回随机元素。

```angular2html
<script type="text/javascript">
_.sample([1, 2, 3, 4]);
// => 2


var array = [1, 2, 3, 4];

function randomArray(array){
    var index = Math.floor(Math.random() * array.length);
    return array[index];
}

console.log(randomArray(array));

// Lodash
console.log(_.sample(array));
console.log(_.sampleSize(array,2));
</script>
```
此外，你也可以指定随机返回元素的个数_.sampleSize(smartTeam,n)，n为需要返回的元素个数

#### 2.3.23、判断对象中是否含有某元素`_.includes(collection, value, [fromIndex=0])`

检查 value(值) 是否在 collection(集合) 中。如果 collection(集合)是一个字符串，那么检查 value（值，子字符串） 是否在字符串中，
否则使用 SameValueZero 做等值比较。 如果指定 fromIndex 是负数，那么从 collection(集合) 的结尾开始检索。

_.includes()第一个参数是需要查询的对象，第二个参数是需要查询的元素，第三个参数是开始查询的下标

* 添加版本
    * 0.1.0
* 参数
    * collection (Array|Object|string): 要检索的集合。
    * value (*): 要检索的值。
    * [fromIndex=0] (number): 要检索的 索引位置。
* 返回
    * (boolean): 如果找到 value 返回 true， 否则返回 false。

```angular2html
<script type="text/javascript">
_.includes([1, 2, 3], 1);
// => true
 
_.includes([1, 2, 3], 1, 2);
// => false
 
_.includes({ 'user': 'fred', 'age': 40 }, 'fred');
// => true
 
_.includes('pebbles', 'eb');
// => true

var smartPerson = {
        'name': '张三',
        'gender': 'male'
    },
smartTeam = ["张三", "李四", "王五", "赵六"];

console.log(_.includes(smartPerson, '张三'));
console.log(_.includes(smartTeam, '李四'));
console.log(_.includes(smartTeam, '李四',2));
</script>
```

#### 2.3.24、检验值是否为空 `_.isEmpty(value)`

检查 value 是否为一个空对象，集合，映射或者set。 判断的依据是除非是有枚举属性的对象，
length 大于 0 的 arguments object, array, string 或类jquery选择器。 

对象如果被认为为空，那么他们没有自己的可枚举属性的对象。 

类数组值，比如arguments对象，array，buffer，string或者类jQuery集合的length 为 0，被认为是空。
类似的，map（映射）和set 的size 为 0，被认为是空。

* 添加版本
    * 0.1.0
* 参数
    * value (*): 要检查的值。
* 返回
    * (boolean): 如果 value 为空，那么返回 true，否则返回 false。

```angular2html
_.isEmpty(null);
// => true
 
_.isEmpty(true);
// => true
 
_.isEmpty(1);
// => true
 
_.isEmpty([1, 2, 3]);
// => false
 
_.isEmpty({ 'a': 1 });
// => false
```

#### 2.3.25、模板插入 `_.template([string=''], [options={}])`

创建一个预编译模板方法，可以插入数据到模板中 "interpolate" 分隔符相应的位置。 HTML会在 "escape" 分隔符中转换为相应实体。
在 "evaluate" 分隔符中允许执行JavaScript代码。 在模板中可以自由访问变量。 如果设置了选项对象，则会优先覆盖 _.templateSettings 的值。

注意: 在开发过程中，构建_.template可以使用 sourceURLs， 便于调试。 

了解更多预编译模板的信息查看 lodash的自定义构建文档。 

了解更多 Chrome 沙箱扩展的信息查看 Chrome的扩展文档。

* 添加版本
    * 0.1.0
* 参数
    * [string=''] (string): 模板字符串.
    * [options={}] (Object): 选项对象.
    * [options.escape=_.templateSettings.escape] (RegExp): "escape" 分隔符.
    * [options.evaluate=_.templateSettings.evaluate] (RegExp): "evaluate" 分隔符.
    * [options.imports=_.templateSettings.imports] (Object): 导入对象到模板中作为自由变量。
    * [options.interpolate=_.templateSettings.interpolate] (RegExp): "interpolate" 分隔符。
    * [options.sourceURL='lodash.templateSources[n]'] (string): 模板编译的来源URL。
    * [options.variable='obj'] (string): 数据对象的变量名。
* 返回
    * (Function): 返回编译模板函数。

```angular2html
// 使用 "interpolate" 分隔符创建编译模板
var compiled = _.template('hello <%= user %>!');
compiled({ 'user': 'fred' });
// => 'hello fred!'
 
// 使用 HTML "escape" 转义数据的值
var compiled = _.template('<b><%- value %></b>');
compiled({ 'value': '<script>' });
// => '<b>&lt;script&gt;</b>'
 
// 使用 "evaluate" 分隔符执行 JavaScript 和 生成HTML代码
var compiled = _.template('<% _.forEach(users, function(user) { %><li><%- user %></li><% }); %>');
compiled({ 'users': ['fred', 'barney'] });
// => '<li>fred</li><li>barney</li>'
 
// 在 "evaluate" 分隔符中使用内部的 `print` 函数
var compiled = _.template('<% print("hello " + user); %>!');
compiled({ 'user': 'barney' });
// => 'hello barney!'
 
// 使用 ES 分隔符代替默认的 "interpolate" 分隔符
var compiled = _.template('hello ${ user }!');
compiled({ 'user': 'pebbles' });
// => 'hello pebbles!'
 
// 使用自定义的模板分隔符
_.templateSettings.interpolate = /{{([\s\S]+?)}}/g;
var compiled = _.template('hello {{ user }}!');
compiled({ 'user': 'mustache' });
// => 'hello mustache!'
 
// 使用反斜杠符号作为纯文本处理
var compiled = _.template('<%= "\\<%- value %\\>" %>');
compiled({ 'value': 'ignored' });
// => '<%- value %>'
 
// 使用 `imports` 选项导入 `jq` 作为 `jQuery` 的别名
var text = '<% jq.each(users, function(user) { %><li><%- user %></li><% }); %>';
var compiled = _.template(text, { 'imports': { 'jq': jQuery } });
compiled({ 'users': ['fred', 'barney'] });
// => '<li>fred</li><li>barney</li>'
 
// 使用 `sourceURL` 选项指定模板的来源URL
var compiled = _.template('hello <%= user %>!', { 'sourceURL': '/basic/greeting.jst' });
compiled(data);
// => 在开发工具的 Sources 选项卡 或 Resources 面板中找到 "greeting.jst"
 
// 使用 `variable` 选项确保在编译模板中不声明变量
var compiled = _.template('hi <%= data.user %>!', { 'variable': 'data' });
compiled.source;
// => function(data) {
//   var __t, __p = '';
//   __p += 'hi ' + ((__t = ( data.user )) == null ? '' : __t) + '!';
//   return __p;
// }
 
// 使用 `source` 特性内联编译模板
// 便以查看行号、错误信息、堆栈
fs.writeFileSync(path.join(cwd, 'jst.js'), '\
  var JST = {\
    "main": ' + _.template(mainText).source + '\
  };\
');
```

#### 2.3.26、筛选属性 `_.pick(object, [props])`

创建一个从 object 中选中的属性的对象。

* 添加版本
    * 0.1.0
* 参数
    * object (Object): 来源对象。
    * [props] (...(string|string[])): 要被忽略的属性。（愚人码头注：单独指定或指定在数组中。）
* 返回
    * (Object): 返回新对象。

```angular2html
var objA = {"name": "colin", "car": "suzuki", "age": 17};
console.log(_.pick(objA, ['car', 'age']));
// => {"car": "suzuki", "age": 17}

var object = { 'a': 1, 'b': '2', 'c': 3 };
_.pick(object, ['a', 'c']);
// => { 'a': 1, 'c': 3 }
```

#### 2.3.26、移除属性 `_.omit(object, [props])`

反向版 _.pick; 这个方法一个对象，这个对象由忽略属性之外的object自身和继承的可枚举属性组成。
（愚人码头注：可以理解为删除object对象的属性）。

* 添加版本
    * 0.1.0
* 参数
    * object (Object): 来源对象。
    * [props] (...(string|string[])): 要被忽略的属性。（愚人码头注：单独指定或指定在数组中。）
* 返回
    * (Object): 返回新对象。

```angular2html
var object = { 'a': 1, 'b': '2', 'c': 3 };
 
_.omit(object, ['a', 'c']);
// => { 'b': '2' }

 var omit = {
     'name': 'lijinglin',
     'height': 175,
     'weight': '95kg'
 }
 var newOmit = _.omit(omit, ['name','height']);
 console.log(omit, newOmit);
 
// => 原数组不变
// => {'name': 'lijinglin', 'height': 175, 'weight': '95kg'} 

// => 清除了数组项；
// => {'height':175}
```

### 2.4、其他工具库推荐

* 前端常用工具：
    * is.js为检查数据类型等提供的小型的js库，大大减少了我们对REGEXP的依赖；
    * underscore.js和lodash.js提供了一整套工具函数，无需经验不足的程序员再去给内置的 JavaScript 对象打补丁；
    * D3.js数据可视化和图表是web应用程序的一种常规需求。当涉及到任何数据操作和可视化时，D3.js 就是事实上的标准。
    它是 GitHub 上最受欢迎的项目之一，并被数百个组织机构所采用。大量的图形、图标和可视化库都是构件于 D3 之上的；D3.js网站
    * three.jsThree.js 提供了一个轻量级的 3D 库，让你可以将 3D 效果渲染成一个 HTML5 的 canvas, SVG, 和 WebGL。
    在three网站上展示了数百个漂亮的实例；
    * lazy.jsLazy.js是类似Underscore或Lo-Dash的JavaScript工具库,但是它有一个非常独特的特性:惰性求值，具有优良的计算性能；
    但是惰性计算会带来其他方便的性能问题，详见注释；故而使用惰性计算需要慎重考虑。

### 2.5、专业词汇解释

惰性计算(Lazy Evaluation)
惰性计算是什么

函数的参数只有在需要计算是才会被计算；
一个函数不需要完全被计算只有需要的部分会被计算；
一个参数只会被计算一次；
惰性计算可以通过避免不必要的计算从而增加程序运行速率；
惰性计算的不足

由于必要的参数或则计算才会被使用，所以惰性计算在运行时，会首先判断是否需要计算，或者是否存在，从而造成另外不必要的开销； 
这会导致在运行一些小的计算时，使得惰性计算并没有必要。
惰性计算在一定程度上可能造成内存泄露； 解释：惰性计算会将所有的参数计算一次，那么惰性计算会将所有计算的参数保存在内存中，
当该参数不再使用后仍然可能会占用内存，这在一定程度堵上造成内存泄露的风险。
前端中的钩子使用：

百度中钩子函数的定义：
钩子函数：钩子函数是Windows消息处理机制的一部分，通过设置“钩子”，应用程序可以在系统级对所有消息、事件进行过滤，
访问在正常情况下无法访问的消息。钩子的本质是一段用以处理系统消息的程序，通过系统调用，把它挂入系统。
我们要讨论的是钩子在lodash中的应用：
我理解的前端中的钩子：

前端中的钩子就是在函数或者页面调用之前对部分函数或页面内的方法进行了统一的处理，从而达到低耦合高内聚的目的；
耦合：一个软件结构内不同模块之间互连程度的度量。
内聚：一个模块内部各个元素彼此结合的紧密程度的度量。
lodash中hook的使用实例：

惰性计算的判断：

在lodash中，处理复杂的对象或者较大的数组时会使用lazy计算从而提高程序的运行性能；在调用lodash的运行方法之前例如
数组、对象、collection方法中的
at , compact , drop , dropRight , dropWhile , filter , find , findLast , head , initial , last , map ,
 reject , reverse , slice , tail , take , takeRight , takeRightWhile , takeWhile , and toArray ；
以及_.chain()方法中的
after , ary , assign , assignIn , assignInWith , assignWith , at , before , bind , bindAll , bindKey ,
 castArray , chain , chunk , commit , compact , concat , conforms , constant , countBy , create , curry ,
  debounce , defaults , defaultsDeep , defer , delay ， difference , differenceBy , differenceWith , drop , 
  dropRight , dropRightWhile , dropWhile , extend 等方法；
在调用这些方法之前会通过islaziable(func){}(版本号4.17.2第6338行)来对这些方法进行处理，从而计算出是否需要惰性计算，
这些是在内部实现的，可以预处理lodash的绝大多数方法；从而增强了lodash的内聚度，而在外部函数中可以随意调用，而在外部随意调用，
不要再处理。从而实现外部模块对随意调用。降低了耦合度。
lodash collection方法的使用：

collection方法中可以传入数组或者对象，lodash会通过getFuncName（）从而计算出你传入的对象，实现对目标对象的解析。
大大增强了lodash中collection的方法的灵活性。

### 2.6 最佳实践

创建一个lodash包装实例，包装value以启用显式链模式。

```
var users = [
  { 'user': 'barney',  'age': 36 },
  { 'user': 'fred',    'age': 40 },
  { 'user': 'pebbles', 'age': 1 }
];

var youngest = _
  .chain(users)
  .sortBy('age')
  .map(function(o) {
    return o.user + ' is ' + o.age;
  })
  .head()
  .value();
// => 'pebbles is 1'
```
一次性解决数据处理

## 3. 同类技术对比

### underscore

Underscore 是一个JavaScript库，它提供了一大堆有用的函数式编程助手，而不需要扩展任何内置对象。

### underscore和lodash的渊源

lodash一开始是Underscore.js库的一个fork，因为和其他(Underscore.js的)贡献者意见相左。
John-David Dalton的最初目标，是提供更多“一致的跨浏览器行为……，并改善性能”。
之后，该项目在现有成功的基础之上取得了更大的成果。最近lodash也发布了3.5版，成为了npm包仓库中依赖最多的库。
它正在摆脱屌丝身份，成为开发者的常规的选择之一。
现在我们所熟知的很多开源项目都已经使用或者转到了lodash阵营之上。
比如JavaScript转译器Babel、博客平台Ghost，和项目脚手架工具Yeoman。
特别Ghost是从Underscore迁移到了lodash，Ghost的创始人John O’Nolan对于此曾评价到：
“这是一个非常明智的选择，它几乎完全是由我们开源开发社区推动的。我们发现lodash包含更多的功能，
更好的性能、恰到好处地使用了semver，并且在Node.js社区（以及其他依赖）中越来越抢眼“。

### lazy

Lazy.js是类似Underscore或Lo-Dash的JavaScript工具库，但是它有一个非常独特的特性：惰性求值。
很多情况下，惰性求值都将带来巨大的性能提升，特别是当处理巨大的数组和连锁使用多个方法的时候

目前lazy和undescore、lodash的性能对比
![lodash、underscore和lazy](http://i.imgur.com/9vP6sVG.png)

This library is experimental and still a work in progress.
这个库还在试验阶段，暂不推荐使用在生产环境

# 参考资料
* [lodash官方文档](https://lodash.com/)
* [博客《lodash入门》作者：前端战五渣](http://www.jianshu.com/p/d46abfa4ddc9)
* [博客《lodash》作者：pinggod](http://www.jianshu.com/p/7436e40ac5d1)
* [lodash中文文档](http://www.css88.com/doc/lodash/#_timesn-iteratee_identity)
* [lodash3.10.1中文文档](http://lodashjs.com/docs/)