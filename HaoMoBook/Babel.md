# Babel

#### 作者：高天阳
#### 邮箱：gty@haomo-studio.com

```
更改历史

* 2018-1-7  高天阳	2.2.2图片改文字
* 2018-1-6  高天阳	格式化文档
* 2017-5-11 高天阳	初始化文档

```

## 1 简介、用途

### 1.1 [简介](http://www.ruanyifeng.com/blog/2016/01/babel.html)

![](../../assets/Babel/babel01.png)

标准的制定者计划，以后每年发布一次标准，使用年份作为版本号。ES6是在2015年发布的，所以又称为ES2015。
但ES6其实多用于泛指ES5.1版本后的下一代JS标准，它涵盖在ES2015版本上稍作改动的ES2016。

Babel是一个广泛使用的转码器，可以将ES6代码转为ES5代码，从而在现有环境执行。

### 1.2 用途

Babel 可用于转化你的 JavaScript 代码

下图的原始代码用了箭头函数

Babel将其转为普通函数

```angular2html
//转码前
input.map(item => item + 1);
//转码后
input.map(function (item){
    return item + 1;
})
```

## 2 安装和使用

### 2.1 安装

#### 2.1.1 配置文件`.babelrc `

[Babel](https://babeljs.io/)的配置文件是.babelrc，存放在项目的根目录下。使用Babel的第一步，就是配置这个文件。

该文件用来设置转码规则和插件，基本格式如下。

```angular2html
{
    "presets": [],
    "plugins": []
}
```

presets字段设定转码规则，官方提供以下的规则集，你可以根据需要安装。

```angular2html
# ES2015转码规则
$ npm install --save-dev babel-preset-es2015

# react转码规则
$ npm install --save-dev babel-preset-react

# ES7不同阶段语法提案的转码规则（共有4个阶段），选装一个
$ npm install --save-dev babel-preset-stage-0
$ npm install --save-dev babel-preset-stage-1
$ npm install --save-dev babel-preset-stage-2
$ npm install --save-dev babel-preset-stage-3
```

然后，将这些规则加入.babelrc。

```angular2html
{
    "presets": [
      "es2015",
      "react",
      "stage-2"
    ],
    "plugins": []
}
```
注意，以下所有Babel工具和模块的使用，都必须先写好.babelrc。

#### 2.1.2 命令行转码babel-cli

Babel提供babel-cli工具，用于命令行转码。

它的安装命令如下。

```angular2html
$ npm install --global babel-cli
```

基本用法如下。

```angular2html
# 转码结果输出到标准输出
$ babel example.js

# 转码结果写入一个文件
# --out-file 或 -o 参数指定输出文件
$ babel example.js --out-file compiled.js
# 或者
$ babel example.js -o compiled.js

# 整个目录转码
# --out-dir 或 -d 参数指定输出目录
$ babel src --out-dir lib
# 或者
$ babel src -d lib

# -s 参数生成source map文件
$ babel src -d lib -s
```

上面代码是在全局环境下，进行Babel转码。这意味着，如果项目要运行，全局环境必须有Babel，也就是说项目产生了对环境的依赖。
另一方面，这样做也无法支持不同项目使用不同版本的Babel。

一个解决办法是将babel-cli安装在项目之中。

```angular2html
# 安装
$ npm install --save-dev babel-cli
```

然后，改写package.json。

```angular2html
{
  // ...
  "devDependencies": {
    "babel-cli": "^6.0.0"
  },
  "scripts": {
    "build": "babel src -d lib"
  },
}
```

转码的时候，就执行下面的命令。

```angular2html
$ npm run build
```

#### 2.1.3 babel-node

babel-cli工具自带一个babel-node命令，提供一个支持ES6的REPL环境。它支持Node的REPL环境的所有功能，而且可以直接运行ES6代码。

它不用单独安装，而是随babel-cli一起安装。然后，执行babel-node就进入PEPL环境。

```angular2html
$ babel-node
> (x => x * 2)(1)
2
```

babel-node命令可以直接运行ES6脚本。将上面的代码放入脚本文件es6.js，然后直接运行。

```angular2html
$ babel-node es6.js
2
```

babel-node也可以安装在项目中。

```angular2html
$ npm install --save-dev babel-cli
```

然后，改写package.json。

```angular2html
{
  "scripts": {
    "script-name": "babel-node script.js"
  }
}
```

上面代码中，使用babel-node替代node，这样script.js本身就不用做任何转码处理。

#### 2.1.4 babel-register

babel-register模块改写require命令，为它加上一个钩子。
此后，每当使用require加载.js、.jsx、.es和.es6后缀名的文件，就会先用Babel进行转码。

```angular2html
$ npm install --save-dev babel-register
```

使用时，必须首先加载babel-register。

```angular2html
require("babel-register");
require("./index.js");
```

然后，就不需要手动对index.js转码了。

需要注意的是，babel-register只会对require命令加载的文件转码，而不会对当前文件转码。
另外，由于它是实时转码，所以只适合在开发环境使用。

#### 2.1.5 babel-core

如果某些代码需要调用Babel的API进行转码，就要使用babel-core模块。

安装命令如下。

```angular2html
$ npm install babel-core --save
```

然后，在项目中就可以调用babel-core。

```angular2html
var babel = require('babel-core');

// 字符串转码
babel.transform('code();', options);
// => { code, map, ast }

// 文件转码（异步）
babel.transformFile('filename.js', options, function(err, result) {
  result; // => { code, map, ast }
});

// 文件转码（同步）
babel.transformFileSync('filename.js', options);
// => { code, map, ast }

// Babel AST转码
babel.transformFromAst(ast, code, options);
// => { code, map, ast }
```

配置对象options，可以参看官方文档http://babeljs.io/docs/usage/options/。

下面是一个例子。

```angular2html
var es6Code = 'let x = n => n + 1';
var es5Code = require('babel-core')
  .transform(es6Code, {
    presets: ['es2015']
  })
  .code;
// '"use strict";\n\nvar x = function x(n) {\n  return n + 1;\n};'
```

上面代码中，transform方法的第一个参数是一个字符串，表示需要转换的ES6代码，第二个参数是转换的配置对象。

#### 2.1.6 babel-polyfill

Babel默认只转换新的JavaScript句法（syntax），而不转换新的API，
比如Iterator、Generator、Set、Maps、Proxy、Reflect、Symbol、Promise等全局对象，
以及一些定义在全局对象上的方法（比如Object.assign）都不会转码。

举例来说，ES6在Array对象上新增了Array.from方法。Babel就不会转码这个方法。
如果想让这个方法运行，必须使用babel-polyfill，为当前环境提供一个垫片。

安装命令如下。

```angular2html
$ npm install --save babel-polyfill
```

然后，在脚本头部，加入如下一行代码。

```angular2html
import 'babel-polyfill';
// 或者
require('babel-polyfill');
```

Babel默认不转码的API非常多，详细清单可以查看babel-plugin-transform-runtime模块的
[definitions.js](https://github.com/babel/babel/blob/master/packages/babel-plugin-transform-runtime/src/definitions.js)文件。

#### 2.1.7 浏览器环境

Babel也可以用于浏览器环境。但是，从Babel 6.0开始，不再直接提供浏览器版本，而是要用构建工具构建出来。
如果你没有或不想使用构建工具，可以通过安装5.x版本的babel-core模块获取。

```angular2html
$ npm install babel-core@old
```

运行上面的命令以后，就可以在当前目录的node_modules/babel-core/子目录里面，
找到babel的浏览器版本browser.js（未精简）和browser.min.js（已精简）。

然后，将下面的代码插入网页。

```angular2html
<script src="node_modules/babel-core/browser.js"></script>
<script type="text/babel">
// Your ES6 code
</script>
```

上面代码中，browser.js是Babel提供的转换器脚本，可以在浏览器运行。
用户的ES6脚本放在script标签之中，但是要注明type="text/babel"。

另一种方法是使用[babel-standalone](https://github.com/Daniel15/babel-standalone)模块提供的浏览器版本，将其插入网页。

```angular2html
<script src="https://cdnjs.cloudflare.com/ajax/libs/babel-standalone/6.4.4/babel.min.js"></script>
<script type="text/babel">
// Your ES6 code
</script>
```

注意，网页中实时将ES6代码转为ES5，对性能会有影响。生产环境需要加载已经转码完成的脚本。

下面是如何将代码打包成浏览器可以使用的脚本，以Babel配合Browserify为例。首先，安装babelify模块。

```angular2html
$ npm install --save-dev babelify babel-preset-es2015
```

然后，再用命令行转换ES6脚本。

```angular2html
$  browserify script.js -o bundle.js \
  -t [ babelify --presets [ es2015 react ] ]
```

上面代码将ES6脚本script.js，转为bundle.js，浏览器直接加载后者就可以了。

在package.json设置下面的代码，就不用每次命令行都输入参数了。

```angular2html
{
  "browserify": {
    "transform": [["babelify", { "presets": ["es2015"] }]]
  }
}
```

#### 2.1.8 在线转换

Babel提供一个[REPL在线编译器](https://babeljs.io/repl/)，可以在线将ES6代码转为ES5代码。转换后的代码，可以直接作为ES5代码插入网页运行。

#### 2.1.9 与其他工具的配合

许多工具需要Babel进行前置转码，这里举两个例子：ESLint和Mocha。

[ESLint](http://eslint.org/) 用于静态检查代码的语法和风格，安装命令如下。

```angular2html
$ npm install --save-dev eslint babel-eslint
```

然后，在项目根目录下，新建一个配置文件.eslint，在其中加入parser字段。

```angular2html
{
  "parser": "babel-eslint",
  "rules": {
    ...
  }
}
```

再在package.json之中，加入相应的scripts脚本。

```angular2html
{
    "name": "my-module",
    "scripts": {
      "lint": "eslint my-files.js"
    },
    "devDependencies": {
      "babel-eslint": "...",
      "eslint": "..."
    }
}
```

[Mocha](http://www.ruanyifeng.com/blog/2015/12/a-mocha-tutorial-of-examples.html) 则是一个测试框架，
如果需要执行使用ES6语法的测试脚本，可以修改package.json的scripts.test。

```angular2html
"scripts": {
  "test": "mocha --ui qunit --compilers js:babel-core/register"
}
```

上面命令中，--compilers参数指定脚本的转码器，规定后缀名为js的文件，都需要使用babel-core/register先转码。

### 2.2 示例

### 2.2.1 创建项目，并引入Babel

Babel在项目根目录中引入

为了将项目的ES6 代码要和ES5 代码区分开
ES6 代码： src 目录下
ES5 代码： lib 目录下。

注：lib 目录应该被加入 .gitignore 文件中

```angular2html
$ mkdir babel
$ cd babel
$ yarn init
$ mkdir src
$ mkdir lib
```

编辑package.json

```angular2html
{
  "name": "babel",
  "version": "1.0.0",
  "main": "index.js",
  "license": "MIT",
  "scripts": {
    "build": "babel src -d lib"
  }
}
```

安装babel-cli

```angular2html
# babel脚手架
$ yarn add babel-cli --dev
# ES2015转码规则
$ yarn add babel-preset-es2015 --dev
# react转码规则
$ yarn add babel-preset-react --dev
# babel的ES7转码规则(ES7不同阶段的语法提案)，选装一个
$ yarn add babel-preset-stage-0 --dev
$ yarn add babel-preset-stage-1 --dev
$ yarn add babel-preset-stage-2 --dev
$ yarn add babel-preset-stage-3 --dev
```

![](../../assets/Babel/babel03.jpeg)  

package.json

```angular2html
{
  "name": "babel",
  "version": "1.0.0",
  "main": "index.js",
  "license": "MIT",
  "scripts": {
    "build": "babel src -d lib"
  },
  "devDependencies": {
    "babel-cli": "^6.26.0",
    "babel-preset-es2015": "^6.24.1",
    "babel-preset-react": "^6.24.1",
    "babel-preset-stage-2": "^6.24.1"
  }
}
```

![](../../assets/Babel/babel04.jpeg)

#### 2.2.2 编写Babel配置文件`.babelrc` 并修改

```angular2html
$ touch .babelrc
```

** es2015 **

使用es2015的，也就是我们常说的es6的相关方法，简单翻译如下，更多细节可以参看[文档](https://babeljs.io/docs/plugins/preset-es2015/)。

* check-es2015-constants // 检验const常量是否被重新赋值
* transform-es2015-arrow-functions // 编译箭头函数
* transform-es2015-block-scoped-functions // 函数声明在作用域内
* transform-es2015-block-scoping // 编译const和let
* transform-es2015-classes // 编译class
* transform-es2015-computed-properties // 编译计算对象属性
* transform-es2015-destructuring // 编译解构赋值
* transform-es2015-duplicate-keys // 编译对象中重复的key，其实是转换成计算对象属性
* transform-es2015-for-of // 编译for...of
* transform-es2015-function-name // 将function.name语义应用于所有的function
* transform-es2015-literals // 编译整数(8进制/16进制)和unicode
* transform-es2015-modules-commonjs // 将modules编译成commonjs
* transform-es2015-object-super // 编译super
* transform-es2015-parameters // 编译参数，包括默认参数，不定参数和解构参数
* transform-es2015-shorthand-properties // 编译属性缩写
* transform-es2015-spread // 编译展开运算符
* transform-es2015-sticky-regex // 正则添加sticky属性
* transform-es2015-template-literals // 编译模版字符串
* transform-es2015-typeof-symbol // 编译Symbol类型
* transform-es2015-unicode-regex // 正则添加unicode模式
* transform-regenerator // 编译generator函数

总结：常用的都覆盖了，并不需要太关心内容，如果使用某些还不支持的语法导致报错，可以回头查一下支持的列表。

** es2016 **

使用es2016的相关插件，也就是es7，更多细节可以参看[文档](https://babeljs.io/docs/plugins/preset-es2016/)。

* transform-exponentiation-operator // 编译幂运算符

** es2017 **

使用es2017的相关插件，也就是es8？，更多细节可以参看[文档](https://babeljs.io/docs/plugins/preset-es2017/)。

* syntax-trailing-function-commas // function最后一个参数允许使用逗号
* transform-async-to-generator // 把async函数转化成generator函数

** latest **

latest是一个特殊的presets，包括了es2015，es2016，es2017的插件（目前为止，以后有es2018也会包括进去）。

** react **

react是一个比较特别的官方推荐的presets，大概是因为比较火吧。加入了flow，jsx等语法，具体可以看[文档](https://babeljs.io/docs/plugins/preset-react/)。

** stage-x(stage-0/1/2/3/4) **

stage-x和上面的es2015等有些类似，但是它是按照JavaScript的提案阶段区分的，一共有5个阶段。而数字越小，阶段越靠后，存在依赖关系。
也就是说stage-0是包括stage-1的，以此类推。

** stage-4 **

已完成的提案，与年度发布的release有关，包含2015年到明年正式发布的内容。
例如，现在是2016年，stage-4应该是包括es2015，es2016，es2017。
经过测试，babel-preset-stage-4这个npm包是不存在的，如果你单纯的需要stage-4的相关方法，
需要引入es2015~es2017的presets。

** stage-3 **

除了stage-4的内容，还包括以下插件，更多细节请看[文档](http://babeljs.io/docs/plugins/preset-stage-3/)。

* transform-object-rest-spread // 编译对象的解构赋值和不定参数
* transform-async-generator-functions // 将async generator function和for await编译为es2015的generator。

** stage-2 **

除了stage-3的内容，还包括以下插件，更多细节请看[文档](http://babeljs.io/docs/plugins/preset-stage-2/)。

* transform-class-properties // 编译静态属性(es2015)和属性初始化语法声明的属性(es2016)。

** stage-1 **

除了stage-2的内容，还包括以下插件，更多细节请看[文档](http://babeljs.io/docs/plugins/preset-stage-1/)。

* transform-class-constructor-call // 编译class中的constructor，在Babel7中会被移除
* transform-export-extensions // 编译额外的exprt语法，如export * as ns from "mod";细节可以看[这个](https://github.com/leebyron/ecmascript-more-export-from)

** stage-0 **

除了stage-1的内容，还包括以下插件，更多细节请看[文档](http://babeljs.io/docs/plugins/preset-stage-0/)。

* transform-do-expressions // 编译do表达式
* transform-function-bind // 编译bind运算符，也就是`::`

** 注意 **

值得我们注意的是

为了统一称呼，我们定义如下：

** 插件名 ** -形如：es2015-arrow-functions、es2015-block-scoped-functions、es2015-block-scoping

** 插件（安装）包名 ** -形如：babel-plugin-transform-es2015-arrow-functions、
babel-plugin-transform-es2015-block-scoped-functions、babel-plugin-transform-es2015-block-scoping

** 配置名 ** -形如：transform-es2015-arrow-functions、transform-es2015-block-scoped-functions、transform-es2015-block-scoping

一般来说，在 .babelrc 中，或者是gulp中，或者是使用babel-standalone 的在线转译功能，都使用的是**配置名**。
一定要区分这三者的区别，不然很容易出错。

```angular2html
{
    "presets": [
      "es2015",
      "react",
      "stage-2"
    ],
    "plugins": []
}
```

#### 2.2.3 编写ES6文件

在src文件夹中创建一些希望转换的js文件吧

```angular2html
let a = 1;

var selected = allJobs.filter(job => job.isSelected());
```

#### 2.2.4 ES6转ES5

```angular2html
$ npm run build
```

![](../../assets/Babel/babel09.jpeg)

### 2.3 最佳实践

#### 2.3.1 本地安装和全局安装

全局安装只需：

```angular2html
$ npm install --global babel-cli
```

这时候我们可以使用 Babel 命令编译文件：

```angular2html
$ babel index.js --out-file compiled.js
#或
$ babel index.js -o compiled.js
```

编译目录：

```angular2html
$ babel src -out-dir lib
#或
babel src -d lib
```

但是，官方推荐本地安装，是这么说的：

> While you can install Babel CLI globally on your machine, it’s much better to install it locally project by project.

> There are two primary reasons for this.

> Different projects on the same machine can depend on different versions of Babel allowing you to update one at a time.

> It means you do not have an implicit dependency on the environment you are working in. Making your project far more portable and easier to setup.

大致的意思就是：可移植性较好并且没有依赖。

本地安装，记在项目的根目录下：

```angular2html
$ npm install --save-dev babel-cli
```
    
但是在本地就不能用 babel 命令了，我们可以在 package.json 文件中添加点东西：

```angular2html
{
    "script": {
        "build": "babel src -d lib"
    }
}
```
    
然后，运行 npm run build 即可把 src 目录编译输出到 lib

#### 2.3.2 编译插件

上述编译其实并没有进行，而是原样输出。这是因为我们没有安装相应的插件，官方提示我们需要安装 babel-reset-es2015 插件：

```angular2html
$ npm install --save-dev babel-preset-es2015
```

然后，在根目录创建一个名为 .babelrc 的文件，里面配置如下内容：

```angular2html
{
    "presets": [
        "es2015"
    ]
}
```
    
同理，可以设置 React 的编译插件：

```angular2html
$ npm install --save-dev babel-preset-react
```
    
.babelrc 文件里即：

```angular2html
{
   "presets": [
       "es2015",
       "react"
   ] 
}
```

#### 2.3.3 babel-polyfill插件

Babel 默认只转换新的 JavaScript 句法（syntax），而不转换新的 API ，比如 Iterator、Generator、Set、Maps、Proxy、
Reflect、Symbol、Promise 等全局对象，以及一些定义在全局对象上的方法（比如 Object.assign）都不会转码。
Babel 默认不转码的 API 非常多，详细清单可以查看 definitions.js 文件

为了完整使用 ES6 的 API ，我们只能安装这个插件：

```angular2html
$ npm install -save-dev babel-polyfill
```
    
然后，在需要使用的文件的顶部引入

```angular2html
import "babel-polyfill"
```
    
node.js 中：

```angular2html
require('babel-polyfill');
```
    
webpack.config.js 中：

```angular2html
module.exports = {
    entry: ['babel-polyfill', './app/js']
}
```

## 参考资料

* [Babel官网](https://babeljs.cn/)
* [阮一峰Babel入门教程](http://www.ruanyifeng.com/blog/2016/01/babel.html)
* [推酷如何使用babel](http://www.tuicool.com/articles/UVb6Zvv)
* [Babel指南&nbsp;-&nbsp;基本环境搭建](https://passport.weibo.com/visitor/visitor?entry=miniblog&a=enter&url=https%3A%2F%2Fweibo.com%2Fp%2F230418d2e38ba80102wn7v&domain=.weibo.com&sudaref=https%3A%2F%2Fwww.baidu.com%2Flink%3Furl%3DUyJNNrh1-_2K82p7-gWDmpx_eVwxQ4qtuOUv7QS_ms6tzliuIotEiDKyezxUaZZlxaf9n-d4oM0GwsVUN2YDJq%26wd%3D%26eqid%3Db67b7ed10000af80000000025a51808e&ua=php-sso_sdk_client-0.6.23&_rand=1515290774.4061)
* [如何写好.babelrc？Babel的presets和plugins配置解析](https://excaliburhan.com/post/babel-preset-and-plugins.html)