### 课堂笔记

代码覆盖率:一个程序的代码被运行程度的量度

基本准则:函数覆盖\(一函数为单位\)、语句覆盖\(以每行代码为单位\)、分支覆盖\(if判断的不同分支-trueORfalse都是不同分支\)、条件覆盖\(会检测到条件中任一条件是否覆盖到\)

Istanbuljs程序的代码覆盖率测试工具

1可检查包括语句、分支的函数覆盖

2命令行工具

3可生成html和lcov报表

# istanbul {#istanbul}

## 第一章 代码覆盖率简介 {#第一章-代码覆盖率简介}

### 1.1 代码覆盖率介绍 {#11-代码覆盖率介绍}

代码覆盖（Code coverage）是用来描述在特定的测试套件\(条件\)下，一个程序的代码被运行程度的量度（一般指比例），具有高的 代码覆盖率（以百分比为单位）的程序，表示在测试期间执行了更多的程序源代码；这表明与具有低代码覆盖率的程序相比，该程序具有较低的可能性检测到程序的bug。

### 1.2 代码覆盖率基本准则 {#12-代码覆盖率基本准则}

* 函数覆盖（Function Coverage）

程序中每一个`function`或者子程序是否被调用到

* 语句覆盖\(Statement Coverage\)

最常用也是最常见的一种覆盖方式，就是度量被测代码中每个可执行语句是否被执行到了，也称作行覆盖

* 分支覆盖\(Branch Coverag\)

度量程序中每一个判定的分支是否被检测到了

* 条件覆盖

每一个字表达是结果为`true`或者`false`是否被检测到了

参考以下的JavaScript的函数

```
  function test(a, b){
    var c =0;
    if(a
>
0 
&
&
 b
>
0){
      c=a;
    }
    return c;
  }

```

假设这个方法使我们某个项目的一个`function`,并且我们使用一些测试套件来测试该函数：

* 测试过程中，该函数至少被调用一次；
* 如调用
  `test(1, 1)`
  ,则满足该函数的语句覆盖，这种情况下执行函数的每一行;
* 如调用
  `test(1, 1)`
  和
  `test(0, 1)`
  ，那么将满足分支覆盖，在第一种情况下，将满足if条件分支，第二种情况，第一个条件
  `a `
  `>`
  ` 0`
  不被满足， 这会阻止执行
  `c=a`
  ;
* 如果调用
  `test(1,0)`
  和
  `test(0,1)`
  ,那么将满足条件覆盖，第一种情况下
  `a`
  `>`
  `0`
  将被满足，第二种情况下
  `b`
  `>`
  `0`
  将被满足

> 满足了条件覆盖并代表满足了分支覆盖；上面的第四种情况，满足了a和b均大于零，但是并不能满足if的true和false两种条件;

## 第二章 istanbul简介 {#第二章-istanbul简介}

Istanbul 是 JavaScript 程序的代码覆盖率检查工具;

### 特性 {#特性}

* 可检查包括语句、分支和函数覆盖，以及反向工程的代码行覆盖
* 命令行工具 可运行带覆盖率检查的 node 单元测试，不需要对测试运行进行协作
* 可生成 HTML 和 LCOV 报表
* 在浏览器和 node 0.4.x, 0.6.x, 0.8.x 上测试通过

## 第三章 Istanbul安装使用 {#第三章-istanbul安装使用}

### 3.1 Istanbul安装 {#31-istanbul安装}

Istanbul 是一个 npm 模块，基于node，使用npm安装即可：

```
$ npm install -g istanbul

```

### 3.2 Istanbul简明实例 {#32-istanbul简明实例}

通过以下实例来了解使用Istanbul来测试代码覆盖率：

有需要测试的脚本文件：test.js, 代码如下：

```
var a = 'istanbul';
function b(){
  console.log('b');
}
function c(i){
  if(i == 'istanbul'){
    return true;
  }else if(i == '123'){
    return false;
  }
}
c(a);

```

命令行使用`istanbul cover`就可以得到覆盖率：

```
$ istanbul cover test.js

```

终端输出如下图所示:

![](https://hxgqh.gitbooks.io/testautomization/content/assets/istanbulTest.png)

返回结果显示，simple.js 有9个语句（statement），执行了6个；有4个分支（branch）， 执行了1个；有2个函数，调用了1个；有9行代码，执行了6行。

这条命令同时还生成了一个 coverage 子目录，其中的 coverage.json 文件包含覆盖率的原始数据，coverage/lcov-report 是可以在浏览器打开的覆盖率报告，其中有详细信息，到底哪些代码没有覆盖到。

![](https://hxgqh.gitbooks.io/testautomization/content/assets/istabulCover.png)

![](https://hxgqh.gitbooks.io/testautomization/content/assets/istanbulReport.png)

### 3.3 覆盖率标准 {#33-覆盖率标准}

完美的覆盖率当然是 100%，但是现实中很难达到。一般会设置一个标准来衡量覆盖率是否达标。

istanbul check-coverage 命令用来设置门槛，同时检查当前代码是否达标。

![](https://hxgqh.gitbooks.io/testautomization/content/assets/istanbulChekeCoverage.png)

上面命令设置语句覆盖率的门槛是 90% ，结果就报错了，因为实际覆盖率只有75%。

除了百分比门槛，我们还可以设置绝对值门槛，比如只允许有一个语句没有被覆盖到。

![](https://hxgqh.gitbooks.io/testautomization/content/assets/istanbulChekCoverage2.png)

上面命令使用负数，表示绝对值门槛。

百分比门槛和绝对值门槛，可以结合使用。

```
$ istanbul check-coverage --statement -5 --branch -3 --function 100

```

上面命令设置了3个覆盖率门槛：5个语句、3个 if 代码块、100%的函数。 注意，这三个门槛是"与"（and）的关系，只要有一个没有达标，就会报错。

### 3.4 与测试框架的结合 {#34-与测试框架的结合}

实际开发时，istanbul 总是与测试框架结合使用，下面以常用的 Mocha 框架为例。

sqrt.js 是一个计算平方根的脚本：

```
var My = {
   sqrt: function(x) {
     if (x 
<
 0) throw new Error("负值没有平方根");
       return Math.exp(Math.log(x)/2);
     }
 };

 module.exports = My;

```

它的测试脚本 test.sqrt.js 放在 test 子目录。

```
var chai = require('chai');
 var expect = chai.expect;
 var My = require('../sqrt.js');

 describe("sqrt", function() {

   it("4的平方根应该等于2", function() {
     expect(My.sqrt(4)).to.equal(2);
   });

   it("参数为负值时应该报错", function() {
     expect(function(){ My.sqrt(-1); }).to.throw("负值没有平方根");
   });

 });

```

然后，执行下面的命令得到代码覆盖率。

![](https://hxgqh.gitbooks.io/testautomization/content/assets/istanbulMocha.png)

上面命令中，istanbul cover 命令后面跟的是 \_mocha 命令，前面的下划线是不能省略的。

因为，mocha 和 \_mocha 是两个不同的命令，前者会新建一个进程执行测试，而后者是在当前进程（即 istanbul 所在的进程）执行测试，只有这样， istanbul 才会捕捉到覆盖率数据。其他测试框架也是如此，必须在同一个进程执行测试。

如果要向 mocha 传入参数，可以写成下面的样子。

```
$ istanbul cover _mocha -- tests/test.sqrt.js -R spec

```

上面命令中，两根连词线后面的部分，都会被当作参数传入 Mocha 。如果不加那两根连词线，它们就会被当作 istanbul 的参数

### 3.5 忽略某些代码 {#35-忽略某些代码}

istanbul 提供注释语法，允许某些代码不计入覆盖率。

```
var object = parameter || /* istanbul ignore next */ {};

```

上面代码是为 object 指定默认值（一个空对象）。如果由于种种原因，没有为 object 为空对象的情况写测试，可以用注释，不将这种情况计入覆盖率。注意，注释要写在"或"运算符的后面。

```
/* istanbul ignore if  */
 if (hardToReproduceError)) {
     return callback(hardToReproduceError);
 }

```

上面代码的 if 语句块，在计算覆盖率的时候会被忽略。

## 参考文档 {#参考文档}

* [代码覆盖率测试工具 istanbul入门](http://www.kancloud.cn/kancloud/istanbul/232927)
* [代码覆盖率](https://en.wikipedia.org/wiki/Code_coverage)



