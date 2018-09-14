# JavaScript标准编码风格

#### 作者：高天阳
#### 邮箱：13683265113@163.com

```
更改历史

* 2018-09-14	    高天阳	初始化文档

```

## 前言

> 什么是编码规范？

编码规范就是指导如何编写和组织代码的一系列标准。通过阅读这些编码规范，你可以知道各个公司的前端开发人员是如何编写代码的。

> 我们为什么需要编码规范？

一个主要原因是：每个人都以不同的方式编写代码。我可能喜欢以某种方式做某件事，而且你可能喜欢以不同的方式去做。
如果我们每个人都只在我们自己的代码上工作，这样并没有什么问题。但是，如果你有一个 10个，100个甚至1000个开发人员的团队，
都在同一个代码库上工作，会发生什么呢？事情变得非常糟糕。 编码规范可以使新开发人员快速掌握代码，然后编写出其他开发人员可以快速轻松理解的代码！

## 1 简介

### 1.1 简介

[JavaScript 标准风格](https://github.com/standard/standard) ，这是一个流行的 JavaScript 风格指南。它可以帮助你减少团队之间的摩擦，增加程序员的幸福感。

这是[一组规则](https://standardjs.com/rules-zhcn.html) ，可以使 JavaScript 代码更加一致 ，
并且可以防止类似于 tabs缩进 和 空格缩进优缺点这一类无聊的话题讨论。你可以采用多种风格之一，并且与其他
（如 [JSLint](http://jslint.com/) ， [JSHint](http://jshint.com/about/) 和 [ESLint](https://eslint.org/docs/rules/) ）
是同一种类型的 JavaScript 检测器。

如果你还不知道什么是linter (检查工具)，或者为什么需要，请查看我们对 [JavaScript 检查(Linting)工具的比较](http://www.css88.com/archives/7593)。

### 1.2 风格的重要性

如果你已经从事编码工作有一段时间了的话，那你肯定会有一种自己喜欢的风格。当你成百上千次以特定的模式编写代码时，
你会发现你的编码方式是令人愉悦的。突然间来了个人，开始把挂在行尾的大括号单起一行。你可能会发牢骚。
深呼吸冷静思考一下，你放置括号的位置或关键字后加空格不会让你的程序更加正确，这只是个人喜好。

每种编程语言都有一种主流编码风格，比如像 Python，官方提供的风格指南被认为是编写程序的正确方式。那么你是否还会继续讨厌缩进用4个空格的人呢？
（愚人码头注：Python 官方提供的风格指南，建议使用4个空格缩进）。

用主流风格进行编码将有助于你的程序更能适应语言的生态环境。您还会发现，如果您熟悉该语言的主流编码风格，并且一开始就同意这种编码风格，
那么您可以更容易地为开源项目贡献代码，同样也更容易让其他人来为你的开源项目贡献代码。

JavaScript 没有官方的编码风格指南，或许 Douglas Crockford 的 The Good Parts 是一个实际上的标准。
他的书（愚人码头注：《JavaScript 语言精粹》）提供了一种编写可靠的方法来 JavaScript 程序，他强调了我们应该积极避免的某些特性。
他发布了 JSLint 来支持这些观点，而其他的检查工具也紧随其后。大多数的检查工具是高度可配置的，让你选择最适合你自己的风格，
并将其强加于别人或团队！JavaScript Standard Style(愚人码头注：这个项目名，所以没翻译，意思为 JavaScript 标准编码风格) 则不同。
你最喜欢的编码风格无关紧要，重要的是，任何选择都可以让每个人理解和合作。

```
采用 standard 编码风格意味着代码清晰性和社区约定的重要性要高于个人的编码风格。这不一定适用于所有项目和开发文化，
但是开放项目源码对于新手来说可能非常不适应。建立清晰的、自动的编码风格，满足贡献者期望可以使项目发展更健康。
```

如果你正在为自己编写一个程序，没有其他人需要为你做贡献，那就使用那些让你最快乐的工具和编码风格。
当你在一个团队中工作时，你应该尽量减少摩擦，保持专业，不要因为小事而浪费太多的时间。

在介绍自己的风格之前，花点时间学习现有代码库的风格。

### 1.3 JavaScript 标准编码风格

* 使用两个空格 – 进行缩进
* 字符串使用单引号 – 需要转义的地方除外
* 不再有冗余的变量 – 这是导致 大量 bug 的源头!
* 无分号 – 这里有3篇文章说明不用分号的好处：[文章1](http://inimino.org/~inimino/blog/javascript_semicolons) [文章2](https://www.youtube.com/watch?v=gsfbh17Ax9I)
* 行首不要以 `(`, `[`, or ``` ` ``` 开头
* 这是省略分号时唯一会造成问题的地方 – 工具里已加了自动检测！
* 关键字后加空格 `if (condition) { ... }`
* 函数名后加空格 `function name (arg) { ... }`
* 坚持使用全等 `===` 摒弃 `==` 一但在需要检查 `null || undefined` 时可以使用  `obj == null`。
* 一定要处理 Node.js 中错误回调传递进来的 `err` 参数。
* 使用浏览器全局变量时加上 `window` 前缀 – `document` 和 `navigator` 除外
* 避免无意中使用到了这些命名看上去很普通的全局变量，`open`, `length`, `event` 还有 `name`。
* 完整的规则列表请参阅下一章节细则

最有争议的规则无疑是不用分号。多年来人们一直认为，始终使用分号是避免错误的最佳实践，Crockford 做了很多工作来促进这一点，
使用封号有很深的根源，在 C 语言里，分号是严格要求的，否则程序不会运行。

JavaScript Standard Style(JavaScript 标准编码风格) 改变了我的想法，不用分号的 JavaScript 非常好。

分号自动插入是 JavaScript 的一个特性，它可以减少噪点、简化程序，我从来没有遇到过由于缺少分号而导致的bug，我也不相信你会遇到。
查看 [JavaScript 中有必需使用分号的吗?](https://www.youtube.com/watch?v=gsfbh17Ax9I) 以了解更多。

并不是所有人都同意，forks semistandard 和 happiness 有点唱反调，强调使用分号。我发现这些 forks 有点伤感，因为它们错过忽略了整个标准的要点。

> **如果我不同意某条规则，可以改吗？**
> 
> 不行。制定这套 `standard` 规范的目的就是让大家都不必再花时间浪费在无谓的代码风格之争上面了。
关于缩进该用制表符还是空格这个问题已经争论了很久了，永远也没有答案。争论这个都可以把需求提前写完了。
遵循 `standard` 规范，你就不用再犹豫了，毕竟不管怎样争论总归会选择一种风格的。希望大家也能在个人语义和普适价值上做一个权衡。

就我个人而言，我已经开始喜欢不使用分号的编码风格了，也许是因为需要编写 Ruby、Python 和 CoffeeScript 的缘故，
这些都不使用分号的语法。无论什么原因，当看不到分号的时候，我发现程序更清晰了。

### 1.4 良好的程序层次结构

程序员应该重视：

1. 正确性
1. 可读性
1. 幸福感
1. 高效率

事实证明，采用 JavaScript Standard Style(JavaScript 标准编码风格)，对以上每一条都有好处。

> 正确性

在所有程序中使用的任何东西，都必须做你想要的，并且没有错误。

编码风格并不会使程序更正确，但是在发布之前，检查工具可以帮你捕获一些错误。

> 可读性

作为一个专业的开发人员，除了提供一份能正常运行的程序代码之外，代码的可读性是最重要的。
阅读和尝试理解程序比编写代码要花费更多的精力和时间，因此请为未来的自己和维护代码的其他人进行可读性优化。

清晰可预测的风格使代码更容易阅读和理解。

> 程序员的幸福感

我喜欢 JavaScript Standard Style(JavaScript 标准编码风格) 的原因之一是，它把重点放在人而不是机器上。
程序员的幸福感在这个列表中排名第三的唯一原因是团队合作中更需要可读性，功能代码的正确性应该放在我们自己的幸福感之前，这是毋庸置疑的。

```
你想享受生活，不是吗？如果你很快就能完成工作，而且你的工作又有趣，那不就是我们想要的享受生活吗？这在一定程度上就是我们生活的目的。你的生活会更加美好。

– Yukihiro Matsumoto （愚人呢码头注：松本行弘是一位日本计算机科学家和程序员。他是Ruby程序设计语言的主要设计者和实现者。）
```

人生苦短，不能因个人偏好的不同而引起意见分歧，设定一个标准并后续推进不是更好吗？如果一个标准的编码风格能够避免团队之间的分歧和摩擦，那么你就会更快乐。

> 高效率

列在最后，但并非最不重要。

如果你必须在这些要点上进行权衡，那么你应该更加重视代码正确性、可读性，并且使程序员对快速编写代码感到愉悦。

计算机处理速度很快。如果程序高效，那就没事了。如果您发现性能不佳，请花时间寻找性能瓶颈并使代码更高效。

人类处理问题的速度相对来说很慢。让事情变得更有效率对我们来说更有价值。采用一种标准编码风格的清晰性使您的代码能够更快地理解并贡献代码。
花在分歧上的时间也少了很多，这是最受欢迎的。

## 2 细则

### 细则目录

1. [使用两个空格进行缩进](#indent)
1. [除需要转义的情况外，字符串统一使用单引号](#quotes)
1. [不要定义未使用的变量](#no-unused-vars)
1. [关键字后面加空格](#keyword-spacing)
1. [函数声明时括号与函数名间加空格](#space-before-function-paren)
1. [始终使用 === 替代 ==](#eqeqeq)
1. [字符串拼接操作符 (Infix operators) 之间要留空格](#space-infix-ops)
1. [逗号后面加空格](#comma-spacing)
1. [else 关键字要与花括号保持在同一行](#brace-style)
1. [多行 if 语句的的括号不能省](#curly)
1. [不要丢掉异常处理中err参数](#handle-callback-err)
1. [使用浏览器全局变量时加上 window. 前缀](#no-undef)
1. [不允许有连续多行空行](#no-multiple-empty-lines)
1. [对于三元运算符 ? 和 : 与他们所负责的代码处于同一行](#operator-linebreak)
1. [每个 var 关键字单独声明一个变量](#one-var)
1. [条件语句中赋值语句使用括号包起来](#no-cond-assign)
1. [单行代码块两边加空格](#block-spacing)
1. [对于变量和函数名统一使用驼峰命名法](#camelcase)
1. [不允许有多余的行末逗号](#comma-dangle)
1. [始终将逗号置于行末](#comma-style)
1. [点号操作符须与属性需在同一行](#dot-location)
1. [文件末尾留一空行](#eol-last)
1. [函数调用时标识符与括号间不留间隔](#func-call-spacing)
1. [键值对当中冒号与值之间要留空白](#key-spacing)
1. [构造函数要以大写字母开头](#new-cap)
1. [无参的构造函数调用时要带上括号](#new-parens)
1. [对象中定义了存值器，一定要对应的定义取值器](#accessor-pairs)
1. [子类的构造器中一定要调用 super](#constructor-super)
1. [使用数组字面量而不是构造器](#no-array-constructor)
1. [避免使用 arguments.callee 和 arguments.caller](#no-caller)
1. [避免对类名重新赋值](#no-class-assign)
1. [避免修改使用 const 声明的变量](#no-const-assign)
1. [避免使用常量作为条件表达式的条件（循环语句除外）](#no-constant-condition)
1. [不要使用 debugger](#no-debugger)
1. [不要对变量使用 delete 操作](#no-delete-var)
1. [不要定义冗余的函数参数](#no-dupe-args)
1. [类中不要定义冗余的属性](#no-dupe-class-members)
1. [对象字面量中不要定义重复的属性](#no-dupe-keys)
1. [switch 语句中不要定义重复的 case 分支](#no-duplicate-case)
1. [同一模块有多个导入时一次性写完](#no-duplicate-imports)
1. [正则中不要使用空字符](#no-empty-character-class)
1. [不要解构空值](#no-empty-pattern)
1. [不要使用 eval()](#no-eval)
1. [catch 中不要对错误重新赋值](#no-ex-assign)
1. [不要扩展原生对象](#no-extend-native)
1. [避免多余的函数上下文绑定](#no-extra-bind)
1. [避免不必要的布尔转换](#no-extra-boolean-cast)
1. [不要使用多余的括号包裹函数](#no-extra-parens)
1. [switch 一定要使用 break 来将条件分支正常中断](#no-fallthrough)
1. [不要省去小数点前面的0](#no-floating-decimal)
1. [避免对声明过的函数重新赋值](#no-func-assign)
1. [不要对全局只读对象重新赋值](#no-global-assign)
1. [注意隐式的 eval()](#no-implied-eval)
1. [嵌套的代码块中禁止再定义函数](#no-inner-declarations)
1. [不要向 RegExp 构造器传入非法的正则表达式](#no-invalid-regexp)
1. [不要使用非法的空白符](#no-irregular-whitespace)
1. [禁止使用 `__iterator__`](#no-iterator)
1. [外部变量不要与对象属性重名](#no-label-var)
1. [不要使用标签语句](#no-labels)
1. [不要书写不必要的嵌套代码块](#no-lone-blocks)
1. [不要混合使用空格与制表符作为缩进](#no-mixed-spaces-and-tabs)
1. [除了缩进，不要使用多个空格](#no-multi-spaces)
1. [不要使用多行字符串](#no-multi-str)
1. [`new` 创建对象实例后需要赋值给变量](#no-new)
1. [禁止使用 `Function` 构造器](#no-new-func)
1. [禁止使用 Object 构造器](#no-new-object)
1. [禁止使用 new require](#no-new-require)
1. [禁止使用 Symbol 构造器](#no-new-symbol)
1. [禁止使用原始包装器](#no-new-wrappers)
1. [不要将全局对象的属性作为函数调用](#no-obj-calls)
1. [不要使用八进制字面量](#no-octal)
1. [字符串字面量中也不要使用八进制转义字符](#no-octal-escape)
1. [使用 `__dirname` 和 `__filename` 时尽量避免使用字符串拼接](#no-path-concat)
1. [使用 `getPrototypeOf` 来替代 `__proto__`](#no-proto)
1. [不要重复声明变量](#no-redeclare)
1. [正则中避免使用多个空格](#no-regex-spaces)
1. [`return` 语句中的赋值必需有括号包裹](#no-return-assign)
1. [避免将变量赋值给自己](#no-self-assign)
1. [避免将变量与自己进行比较操作](#no-self-compare)
1. [避免使用逗号操作符](#no-sequences)
1. [不要随意更改关键字的值](#no-shadow-restricted-names)
1. [禁止使用稀疏数组（Sparse arrays）](#no-sparse-arrays)
1. [不要使用制表符](#no-tabs)
1. [正确使用 ES6 中的字符串模板](#no-template-curly-in-string)
1. [使用 `this` 前请确保 `super()` 已调用](#no-this-before-super)
1. [用 `throw` 抛错时，抛出 `Error` 对象而不是字符串](#no-throw-literal)
1. [行末不留空格](#no-trailing-spaces)
1. [不要使用 `undefined` 来初始化变量](#no-undef-init)
1. [循环语句中注意更新循环变量](#no-unmodified-loop-condition)
1. [如果有更好的实现，尽量不要使用三元表达式](#no-unneeded-ternary)
1. [`return`，`throw`，`continue` 和 `break` 后不要再跟代码](#no-unreachable)
1. [`finally` 代码块中不要再改变程序执行流程](#no-unsafe-finally)
1. [关系运算符的左值不要做取反操作](#no-unsafe-negation)
1. [避免不必要的 `.call()` 和 `.apply()`](#no-useless-call)
1. [避免使用不必要的计算值作对象属性](#no-useless-computed-key)
1. [禁止多余的构造器](#no-useless-constructor)
1. [禁止不必要的转义](#no-useless-escape)
1. [`import`, `export` 和解构操作中，禁止赋值到同名变量](#no-useless-rename)
1. [属性前面不要加空格](#no-whitespace-before-property)
1. [禁止使用 `with`](#no-with)
1. [对象属性换行时注意统一代码风格](#object-property-newline)
1. [代码块中避免多余留白](#padded-blocks)
1. [展开运算符与它的表达式间不要留空白](#rest-spread-spacing)
1. [遇到分号时空格要后留前不留](#semi-spacing)
1. [代码块首尾留空格](#space-before-blocks)
1. [圆括号间不留空格](#space-in-parens)
1. [一元运算符后面跟一个空格](#space-unary-ops)
1. [注释首尾留空格](#spaced-comment)
1. [模板字符串中变量前后不加空格](#template-curly-spacing)
1. [检查 `NaN` 的正确姿势是使用 `isNaN()`](#use-isnan)
1. [用合法的字符串跟 `typeof` 进行比较操作](#valid-typeof)
1. [自调用匿名函数 (IIFEs) 使用括号包裹](#wrap-iife)
1. [yield * 中的 * 前后都要有空格](#yield-star-spacing)
1. [请书写优雅的条件语句（avoid Yoda conditions）](#yoda)

### 2.1 使用两个空格进行缩进{#indent}

eslint: indent

```
function hello (name) {
  console.log('hi', name)
}
```

### 2.2 除需要转义的情况外，字符串统一使用单引号{#quotes}

eslint: quotes

```
console.log('hello there')
$("<div class='box'>")
```

### 2.3 不要定义未使用的变量{#no-unused-vars}

eslint: no-unused-vars

```
function myFunction () {
  var result = something()   // ✗ avoid
}
```

### 2.4 关键字后面加空格{#keyword-spacing}

eslint: keyword-spacing

```
if (condition) { ... }   // ✓ ok
if(condition) { ... }    // ✗ avoid
```

### 2.5 函数声明时括号与函数名间加空格{#space-before-function-paren}

eslint: space-before-function-paren

```
function name (arg) { ... }   // ✓ ok
function name(arg) { ... }    // ✗ avoid
 
run(function () { ... })      // ✓ ok
run(function() { ... })       // ✗ avoid
```

### 2.6 始终使用 === 替代 =={#eqeqeq}

例外： obj == null 可以用来检查 null || undefined。

eslint: eqeqeq

```
if (name === 'John')   // ✓ ok
if (name == 'John')    // ✗ avoid
```

```
if (name !== 'John')   // ✓ ok
if (name != 'John')    // ✗ avoid
```

### 2.7 字符串拼接操作符 (Infix operators) 之间要留空格{#space-infix-ops}

eslint: space-infix-ops

```
// ✓ ok
var x = 2
var message = 'hello, ' + name + '!'
```

```
// ✗ avoid
var x=2
var message = 'hello, '+name+'!'
```

### 2.8 逗号后面加空格{#comma-spacing}

eslint: comma-spacing

```
// ✓ ok
var list = [1, 2, 3, 4]
function greet (name, options) { ... }
```

```
// ✗ avoid
var list = [1,2,3,4]
function greet (name,options) { ... }
```

### 2.9 else 关键字要与花括号保持在同一行{#brace-style}

eslint: brace-style

```
// ✓ ok
if (condition) {
  // ...
} else {
  // ...
}
```

```
// ✗ avoid
if (condition)
{
  // ...
}
else
{
  // ...
}
```

### 2.10 多行 if 语句的的括号不能省{#curly}

eslint: curly

```
// ✓ ok
if (options.quiet !== true) console.log('done')
```

```
// ✓ ok
if (options.quiet !== true) {
  console.log('done')
}
```

```
// ✗ avoid
if (options.quiet !== true)
  console.log('done')
```

### 2.11 不要丢掉异常处理中err参数{#handle-callback-err}

eslint: handle-callback-err

```
// ✓ ok
run(function (err) {
  if (err) throw err
  window.alert('done')
})
```

```
// ✗ avoid
run(function (err) {
  window.alert('done')
})
```

### 2.12 使用浏览器全局变量时加上 window. 前缀{#no-undef}

Exceptions are: document, console and navigator.

eslint: no-undef

```
window.alert('hi')   // ✓ ok
```

### 2.13 不允许有连续多行空行{#no-multiple-empty-lines}

eslint: no-multiple-empty-lines

```
// ✓ ok
var value = 'hello world'
console.log(value)
```

```
// ✗ avoid
var value = 'hello world'
 
 
console.log(value)
```

### 2.14 对于三元运算符 ? 和 : 与他们所负责的代码处于同一行{#operator-linebreak}

eslint: operator-linebreak

```
// ✓ ok
var location = env.development ? 'localhost' : 'www.api.com'
 
// ✓ ok
var location = env.development
  ? 'localhost'
  : 'www.api.com'
 
// ✗ avoid
var location = env.development ?
  'localhost' :
  'www.api.com'
```

### 2.15 每个 var 关键字单独声明一个变量{#one-var}

eslint: one-var

```
// ✓ ok
var silent = true
var verbose = true
 
// ✗ avoid
var silent = true, verbose = true
 
// ✗ avoid
var silent = true,
    verbose = true
```

### 2.16 条件语句中赋值语句使用括号包起来。这样使得代码更加清晰可读，而不会认为是将条件判断语句的全等号（===）错写成了等号（=）{#no-cond-assign}

eslint: no-cond-assign

```
// ✓ ok
while ((m = text.match(expr))) {
  // ...
}
 
// ✗ avoid
while (m = text.match(expr)) {
  // ...
}
```

### 2.17 单行代码块两边加空格{#block-spacing}

eslint: block-spacing

```
function foo () {return true}    // ✗ avoid
function foo () { return true }  // ✓ ok
```

### 2.18 对于变量和函数名统一使用驼峰命名法{#camelcase}

eslint: camelcase

```
function my_function () { }    // ✗ avoid
function myFunction () { }     // ✓ ok

var my_var = 'hello'           // ✗ avoid
var myVar = 'hello'            // ✓ ok
```

### 2.19 不允许有多余的行末逗号{#comma-dangle}

eslint: comma-dangle

```
var obj = {
  message: 'hello',   // ✗ avoid
}
```

### 2.20 始终将逗号置于行末{#comma-style}

eslint: comma-style

```
var obj = {
  foo: 'foo'
  ,bar: 'bar'   // ✗ avoid
}

var obj = {
  foo: 'foo',
  bar: 'bar'   // ✓ ok
}
```

### 2.21 点号操作符须与属性需在同一行{#dot-location}

eslint: dot-location

```
console.
  log('hello')  // ✗ avoid

console
  .log('hello') // ✓ ok
```

### 2.22 文件末尾留一空行{#eol-last}

eslint: eol-last

### 2.23 函数调用时标识符与括号间不留间隔{#func-call-spacing}

eslint: func-call-spacing

```
console.log ('hello') // ✗ avoid
console.log('hello')  // ✓ ok
```

### 2.24 键值对当中冒号与值之间要留空白{#key-spacing}

eslint: key-spacing

```
var obj = { 'key' : 'value' }    // ✗ avoid
var obj = { 'key' :'value' }     // ✗ avoid
var obj = { 'key':'value' }      // ✗ avoid
var obj = { 'key': 'value' }     // ✓ ok
```

### 2.25 构造函数要以大写字母开头{#new-cap}

eslint: new-cap

```
function animal () {}
var dog = new animal()    // ✗ avoid

function Animal () {}
var dog = new Animal()    // ✓ ok
```

### 2.26 无参的构造函数调用时要带上括号{#new-parens}

eslint: new-parens

```
function Animal () {}
var dog = new Animal    // ✗ avoid
var dog = new Animal()  // ✓ ok
```

### 2.27 对象中定义了存值器，一定要对应的定义取值器{#accessor-pairs}

eslint: accessor-pairs

```
var person = {
  set name (value) {    // ✗ avoid
    this._name = value
  }
}

var person = {
  set name (value) {
    this._name = value
  },
  get name () {         // ✓ ok
    return this._name
  }
}
```

### 2.28 子类的构造器中一定要调用 super{#constructor-super}

eslint: constructor-super

```
class Dog {
  constructor () {
    super()   // ✗ avoid
  }
}

class Dog extends Mammal {
  constructor () {
    super()   // ✓ ok
  }
}
```

### 2.29 使用数组字面量而不是构造器{#no-array-constructor}

eslint: no-array-constructor

```
var nums = new Array(1, 2, 3)   // ✗ avoid
var nums = [1, 2, 3]            // ✓ ok
```

### 2.30 避免使用 arguments.callee 和 arguments.caller{#no-caller}

eslint: no-caller

```
function foo (n) {
  if (n <= 0) return

  arguments.callee(n - 1)   // ✗ avoid
}

function foo (n) {
  if (n <= 0) return

  foo(n - 1)
}
```

### 2.31 避免对类名重新赋值{#no-class-assign}

eslint: no-class-assign

```
class Dog {}
Dog = 'Fido'    // ✗ avoid
```

### 2.32 避免修改使用 const 声明的变量{#no-const-assign}

eslint: no-const-assign

```
const score = 100
score = 125       // ✗ avoid
```

### 2.33 避免使用常量作为条件表达式的条件（循环语句除外）{#no-constant-condition}

eslint: no-constant-condition

```
if (false) {    // ✗ avoid
  // ...
}

if (x === 0) {  // ✓ ok
  // ...
}

while (true) {  // ✓ ok
  // ...
}
```

### 2.34 不要使用 debugger{#no-debugger}

eslint: no-debugger

```
function sum (a, b) {
  debugger      // ✗ avoid
  return a + b
}
```

### 2.35 不要对变量使用 delete 操作{#no-delete-var}

eslint: no-delete-var

```
var name
delete name     // ✗ avoid
```

### 2.36 不要定义冗余的函数参数{#no-dupe-args}

eslint: no-dupe-args

```
function sum (a, b, a) {  // ✗ avoid
  // ...
}

function sum (a, b, c) {  // ✓ ok
  // ...
}
```

### 2.37 类中不要定义冗余的属性{#no-dupe-class-members}

eslint: no-dupe-class-members

```
class Dog {
  bark () {}
  bark () {}    // ✗ avoid
}
```

### 2.38 对象字面量中不要定义重复的属性{#no-dupe-keys}

eslint: no-dupe-keys

```
var user = {
  name: 'Jane Doe',
  name: 'John Doe'    // ✗ avoid
}
```

### 2.39 switch 语句中不要定义重复的 case 分支{#no-duplicate-case}

eslint: no-duplicate-case

```
switch (id) {
  case 1:
    // ...
  case 1:     // ✗ avoid
}
```

### 2.40 同一模块有多个导入时一次性写完{#no-duplicate-imports}

eslint: no-duplicate-imports

```
import { myFunc1 } from 'module'
import { myFunc2 } from 'module'          // ✗ avoid

import { myFunc1, myFunc2 } from 'module' // ✓ ok
```

### 2.41 正则中不要使用空字符{#no-empty-character-class}

eslint: no-empty-character-class

```
const myRegex = /^abc[]/      // ✗ avoid
const myRegex = /^abc[a-z]/   // ✓ ok
```

### 2.42 不要解构空值{#no-empty-pattern}

eslint: no-empty-pattern

```
const { a: {} } = foo         // ✗ avoid
const { a: { b } } = foo      // ✓ ok
```

### 2.43 不要使用 eval(){#no-eval}

eslint: no-eval

```
eval( "var result = user." + propName ) // ✗ avoid
var result = user[propName]             // ✓ ok
```

### 2.44 catch 中不要对错误重新赋值{#no-ex-assign}

eslint: no-ex-assign

```
try {
  // ...
} catch (e) {
  e = 'new value'             // ✗ avoid
}

try {
  // ...
} catch (e) {
  const newVal = 'new value'  // ✓ ok
}
```

### 2.45 不要扩展原生对象{#no-extend-native}

eslint: no-extend-native

```
Object.prototype.age = 21     // ✗ avoid
```

### 2.46 避免多余的函数上下文绑定{#no-extra-bind}

eslint: no-extra-bind

```
const name = function () {
  getName()
}.bind(user)    // ✗ avoid

const name = function () {
  this.getName()
}.bind(user)    // ✓ ok
```

### 2.47 避免不必要的布尔转换{#no-extra-boolean-cast}

eslint: no-extra-boolean-cast

```
const result = true
if (!!result) {   // ✗ avoid
  // ...
}

const result = true
if (result) {     // ✓ ok
  // ...
}
```

### 2.48 不要使用多余的括号包裹函数{#no-extra-parens}

eslint: no-extra-parens

```
const myFunc = (function () { })   // ✗ avoid
const myFunc = function () { }     // ✓ ok
```

### 2.49 switch 一定要使用 break 来将条件分支正常中断{#no-fallthrough}

eslint: no-fallthrough

```
switch (filter) {
  case 1:
    doSomething()    // ✗ avoid
  case 2:
    doSomethingElse()
}

switch (filter) {
  case 1:
    doSomething()
    break           // ✓ ok
  case 2:
    doSomethingElse()
}

switch (filter) {
  case 1:
    doSomething()
    // fallthrough  // ✓ ok
  case 2:
    doSomethingElse()
}
```

### 2.50 不要省去小数点前面的0{#no-floating-decimal}

eslint: no-floating-decimal

```
const discount = .5      // ✗ avoid
const discount = 0.5     // ✓ ok
```

### 2.51 避免对声明过的函数重新赋值{#no-func-assign}

eslint: no-func-assign

```
function myFunc () { }
myFunc = myOtherFunc    // ✗ avoid
```

### 2.52 不要对全局只读对象重新赋值{#no-global-assign}

eslint: no-global-assign

```
window = {}     // ✗ avoid
```

### 2.53 注意隐式的 eval(){#no-implied-eval}

eslint: no-implied-eval

```
setTimeout("alert('Hello world')")                   // ✗ avoid
setTimeout(function () { alert('Hello world') })     // ✓ ok
```

### 2.54 嵌套的代码块中禁止再定义函数{#no-inner-declarations}

eslint: no-inner-declarations

```
if (authenticated) {
  function setAuthUser () {}    // ✗ avoid
}
```

### 2.55 不要向 RegExp 构造器传入非法的正则表达式{#no-invalid-regexp}

eslint: no-invalid-regexp

```
RegExp('[a-z')    // ✗ avoid
RegExp('[a-z]')   // ✓ ok
```

### 2.56 不要使用非法的空白符{#no-irregular-whitespace}

eslint: no-irregular-whitespace

```
function myFunc () /*<NBSP>*/{}   // ✗ avoid
```

### 2.57 禁止使用 `__iterator__`{#no-iterator}

eslint: no-iterator

```
Foo.prototype.__iterator__ = function () {}   // ✗ avoid
```

### 2.58 外部变量不要与对象属性重名{#no-label-var}

eslint: no-label-var

```
var score = 100
function game () {
  score: while (true) {      // ✗ avoid
    score -= 10
    if (score > 0) continue score
    break
  }
}
```

### 2.59 不要使用标签语句{#no-labels}

eslint: no-labels

```
label:
  while (true) {
    break label     // ✗ avoid
  }
```

### 2.60 不要书写不必要的嵌套代码块{#no-lone-blocks}

eslint: no-lone-blocks

```
function myFunc () {
  {                   // ✗ avoid
    myOtherFunc()
  }
}

function myFunc () {
  myOtherFunc()       // ✓ ok
}
```

### 2.61 不要混合使用空格与制表符作为缩进{#no-mixed-spaces-and-tabs}

eslint: no-mixed-spaces-and-tabs

### 2.62 除了缩进，不要使用多个空格{#no-multi-spaces}

eslint: no-multi-spaces

```
const id =    1234    // ✗ avoid
const id = 1234       // ✓ ok
```

### 2.63 不要使用多行字符串{#no-multi-str}

eslint: no-multi-str

```
const message = 'Hello \
                 world'     // ✗ avoid
```

### 2.64 `new` 创建对象实例后需要赋值给变量{#no-new}

eslint: no-new

```
new Character()                     // ✗ avoid
const character = new Character()   // ✓ ok
```

### 2.65 禁止使用 `Function` 构造器{#no-new-func}

eslint: no-new-func

```
var sum = new Function('a', 'b', 'return a + b')    // ✗ avoid
```

### 2.66 禁止使用 Object 构造器{#no-new-object}

eslint: no-new-object

```
let config = new Object()   // ✗ avoid
```

### 2.67 禁止使用 new require{#no-new-require}

eslint: no-new-require

```
const myModule = new require('my-module')    // ✗ avoid
```

### 2.68 禁止使用 Symbol 构造器{#no-new-symbol}

eslint: no-new-symbol

```
const foo = new Symbol('foo')   // ✗ avoid
```

### 2.69 禁止使用原始包装器{#no-new-wrappers}

eslint: no-new-wrappers

```
const message = new String('hello')   // ✗ avoid
```

### 2.70 不要将全局对象的属性作为函数调用{#no-obj-calls}

eslint: no-obj-calls

```
const math = Math()   // ✗ avoid
```

### 2.71 不要使用八进制字面量{#no-octal}

eslint: no-octal

```
const num = 042     // ✗ avoid
const num = '042'   // ✓ ok
```

### 2.72 字符串字面量中也不要使用八进制转义字符{#no-octal-escape}

eslint: no-octal-escape

```
const copyright = 'Copyright \251'  // ✗ avoid
```

### 2.73 使用 `__dirname` 和 `__filename` 时尽量避免使用字符串拼接{#no-path-concat}

eslint: no-path-concat

```
const pathToFile = __dirname + '/app.js'            // ✗ avoid
const pathToFile = path.join(__dirname, 'app.js')   // ✓ ok
```
### 2.74 使用 `getPrototypeOf` 来替代 `__proto__`{#no-proto}

eslint: no-proto

```
const foo = obj.__proto__               // ✗ avoid
const foo = Object.getPrototypeOf(obj)  // ✓ ok
```
### 2.75 不要重复声明变量{#no-redeclare}

eslint: no-redeclare

```
let name = 'John'
let name = 'Jane'     // ✗ avoid

let name = 'John'
name = 'Jane'         // ✓ ok
```

### 2.76 正则中避免使用多个空格{#no-regex-spaces}

eslint: no-regex-spaces

```
const regexp = /test   value/   // ✗ avoid

const regexp = /test {3}value/  // ✓ ok
const regexp = /test value/     // ✓ ok
```

### 2.77 `return` 语句中的赋值必需有括号包裹{#no-return-assign}

eslint: no-return-assign

```
function sum (a, b) {
  return result = a + b     // ✗ avoid
}

function sum (a, b) {
  return (result = a + b)   // ✓ ok
}
```

### 2.78 避免将变量赋值给自己{#no-self-assign}

eslint: no-self-assign

```
name = name   // ✗ avoid
```

### 2.79 避免将变量与自己进行比较操作{#no-self-compare}

eslint: no-self-compare

```
if (score === score) {}   // ✗ avoid
```

### 2.80 避免使用逗号操作符{#no-sequences}

eslint: no-sequences

```
if (doSomething(), !!test) {}   // ✗ avoid
```

### 2.81 不要随意更改关键字的值{#no-shadow-restricted-names}

eslint: no-shadow-restricted-names

```
let undefined = 'value'     // ✗ avoid
```

### 2.82 禁止使用稀疏数组（Sparse arrays）{#no-sparse-arrays}

eslint: no-sparse-arrays

```
let fruits = ['apple',, 'orange']       // ✗ avoid
```

### 2.83 不要使用制表符{#no-tabs}

eslint: no-tabs

### 2.84 正确使用 ES6 中的字符串模板{#no-template-curly-in-string}

eslint: no-template-curly-in-string

```
const message = 'Hello ${name}'   // ✗ avoid
const message = `Hello ${name}`   // ✓ ok
```

### 2.85 使用 `this` 前请确保 `super()` 已调用{#no-this-before-super}

eslint: no-this-before-super

```
class Dog extends Animal {
  constructor () {
    this.legs = 4     // ✗ avoid
    super()
  }
}
```

### 2.86 用 `throw` 抛错时，抛出 `Error` 对象而不是字符串{#no-throw-literal}

eslint: no-throw-literal

```
throw 'error'               // ✗ avoid
throw new Error('error')    // ✓ ok
```

### 2.87 行末不留空格{#no-trailing-spaces}

eslint: no-trailing-spaces

### 2.88 不要使用 `undefined` 来初始化变量{#no-undef-init}

eslint: no-undef-init

```
let name = undefined    // ✗ avoid

let name
name = 'value'          // ✓ ok
```

### 2.89 循环语句中注意更新循环变量{#no-unmodified-loop-condition}

eslint: no-unmodified-loop-condition

```
for (let i = 0; i < items.length; j++) {...}    // ✗ avoid
for (let i = 0; i < items.length; i++) {...}    // ✓ ok
```

### 2.90 如果有更好的实现，尽量不要使用三元表达式{#no-unneeded-ternary}

eslint: no-unneeded-ternary

```
let score = val ? val : 0     // ✗ avoid
let score = val || 0          // ✓ ok
```

### 2.91 `return`，`throw`，`continue` 和 `break` 后不要再跟代码{#no-unreachable}

eslint: no-unreachable

```
function doSomething () {
  return true
  console.log('never called')     // ✗ avoid
}
```

### 2.92 `finally` 代码块中不要再改变程序执行流程{#no-unsafe-finally}

eslint: no-unsafe-finally

```
try {
  // ...
} catch (e) {
  // ...
} finally {
  return 42     // ✗ avoid
}
```

### 2.93 关系运算符的左值不要做取反操作{#no-unsafe-negation}

eslint: no-unsafe-negation

```
if (!key in obj) {}       // ✗ avoid
```

### 2.94 避免不必要的 `.call()` 和 `.apply()`{#no-useless-call}

eslint: no-useless-call

```
sum.call(null, 1, 2, 3)   // ✗ avoid
```

### 2.95 避免使用不必要的计算值作对象属性{#no-useless-computed-key}

eslint: no-useless-computed-key

```
const user = { ['name']: 'John Doe' }   // ✗ avoid
const user = { name: 'John Doe' }       // ✓ ok
```

### 2.96 禁止多余的构造器{#no-useless-constructor}

eslint: no-useless-constructor

```
class Car {
  constructor () {      // ✗ avoid
  }
}
```

### 2.97 禁止不必要的转义{#no-useless-escape}

eslint: no-useless-escape

```
let message = 'Hell\o'  // ✗ avoid
```

### 2.98 `import`, `export` 和解构操作中，禁止赋值到同名变量{#no-useless-rename}

eslint: no-useless-rename

```
import { config as config } from './config'     // ✗ avoid
import { config } from './config'               // ✓ ok
```

### 2.99 属性前面不要加空格{#no-whitespace-before-property}

eslint: no-whitespace-before-property

```
user .name      // ✗ avoid
user.name       // ✓ ok
```

### 2.100 禁止使用 `with`{#no-with}

eslint: no-with

```
with (val) {...}    // ✗ avoid
```

### 2.101 对象属性换行时注意统一代码风格{#object-property-newline}

eslint: object-property-newline

```
const user = {
  name: 'Jane Doe', age: 30,
  username: 'jdoe86'            // ✗ avoid
}

const user = { name: 'Jane Doe', age: 30, username: 'jdoe86' }    // ✓ ok

const user = {
  name: 'Jane Doe',
  age: 30,
  username: 'jdoe86'
}  
```

### 2.102 代码块中避免多余留白{#padded-blocks}

eslint: padded-blocks

```
if (user) {
                            // ✗ avoid
  const name = getName()

}

if (user) {
  const name = getName()    // ✓ ok
}
```

### 2.103 展开运算符与它的表达式间不要留空白{#rest-spread-spacing}

eslint: rest-spread-spacing

```
fn(... args)    // ✗ avoid
fn(...args)     // ✓ ok
```

### 2.104 遇到分号时空格要后留前不留{#semi-spacing}

eslint: semi-spacing

```
for (let i = 0 ;i < items.length ;i++) {...}    // ✗ avoid
for (let i = 0; i < items.length; i++) {...}    // ✓ ok
```

### 2.105 代码块首尾留空格{#space-before-blocks}

eslint: space-before-blocks

```
if (admin){...}     // ✗ avoid
if (admin) {...}    // ✓ ok
```

### 2.106 圆括号间不留空格{#space-in-parens}

eslint: space-in-parens

```
getName( name )     // ✗ avoid
getName(name)       // ✓ ok
```

### 2.107 一元运算符后面跟一个空格{#space-unary-ops}

eslint: space-unary-ops

```
typeof!admin        // ✗ avoid
typeof !admin        // ✓ ok
```

### 2.108 注释首尾留空格{#spaced-comment}

eslint: spaced-comment

```
//comment           // ✗ avoid
// comment          // ✓ ok

/*comment*/         // ✗ avoid
/* comment */       // ✓ ok
```

### 2.109 模板字符串中变量前后不加空格{#template-curly-spacing}

eslint: template-curly-spacing

```
const message = `Hello, ${ name }`    // ✗ avoid
const message = `Hello, ${name}`      // ✓ ok
```

### 2.110 检查 `NaN` 的正确姿势是使用 `isNaN()`{#use-isnan}

eslint: use-isnan

```
if (price === NaN) { }      // ✗ avoid
if (isNaN(price)) { }       // ✓ ok
```

### 2.111 用合法的字符串跟 `typeof` 进行比较操作{#valid-typeof}

eslint: valid-typeof

```
typeof name === 'undefimed'     // ✗ avoid
typeof name === 'undefined'     // ✓ ok
```

### 2.112 自调用匿名函数 (IIFEs) 使用括号包裹{#wrap-iife}

eslint: wrap-iife

```
const getName = function () { }()     // ✗ avoid

const getName = (function () { }())   // ✓ ok
const getName = (function () { })()   // ✓ ok
```

### 2.113 yield * 中的 * 前后都要有空格{#yield-star-spacing}

eslint: yield-star-spacing

```
yield* increment()    // ✗ avoid
yield * increment()   // ✓ ok

```

### 2.114 请书写优雅的条件语句（avoid Yoda conditions）{#yoda}

eslint: yoda

```
if (42 === age) { }    // ✗ avoid
if (age === 42) { }    // ✓ ok
```

## 3 关于分号

### 3.1 不要使用分号 (参见：1，2，3)

eslint: semi

```
window.alert('hi')   // ✓ ok
window.alert('hi');  // ✗ avoid
```

### 3.2 不要使用 `(`, `[`, or ``` ` ``` 等作为一行的开始。在没有分号的情况下代码压缩后会导致报错，而坚持这一规范则可避免出错

eslint: no-unexpected-multiline

```
// ✓ ok
;(function () {
  window.alert('ok')
}())
```

```
// ✗ avoid
(function () {
  window.alert('ok')
}())
// ✓ ok
;[1, 2, 3].forEach(bar)
```

```
// ✗ avoid
[1, 2, 3].forEach(bar)
// ✓ ok
;`hello`.indexOf('o')

// ✗ avoid
`hello`.indexOf('o')
```
备注：上面的写法只能说聪明过头了。

相比更加可读易懂的代码，那些看似投巧的写法是不可取的。

譬如：

```
;[1, 2, 3].forEach(bar)
```

建议的写法是：

```
var nums = [1, 2, 3]
nums.forEach(bar)
```

## 4 同类型技术比较

> Airbnb JavaScript Style Guide

```
一份最合理的 JavasScript 编码规范。
```

Airbnb 的这份编码规范是互联网上最受欢迎的 JavaScript 编码规范之一。 它几乎涵盖了 JavaScript 的各个方面。

* [阅读地址](https://github.com/airbnb/javascript) 
* [中文翻译](http://www.css88.com/archives/8345)

> Google JavaScript Style Guide

```
只有遵守了这里的规则，一个 JavaScript 源文件才能被称为“Google Style”。
```

* [阅读地址](https://google.github.io/styleguide/jsguide.html) 

> Idiomatic JavaScript Style Guide

```
不管有多少人贡献，任何代码库中的所有代码看起来应该像同一个人写的。
```

另一个最流行的 JavaScript 编码规范，该编码规范有多种语言版本。

* [阅读地址](https://github.com/rwaldron/idiomatic.js) 

> JavaScript Standard Style Guide

```
一份强大的 JavaScript 编码规范，自带 linter 和自动代码纠正。 没有配置。 自动格式化代码。 可以在编码早期就发现规范问题和低级错误。
```

这份编码规范被很多知名公司所采用，比如 NPM、GitHub、mongoDB 和 ZenDesk 等。

* [阅读地址](https://github.com/standard/standard) 

> jQuery JavaScript Style Guide

要向 jQuery 提交一些代码，来帮助使 jQuery 更好？阅读他们的编码规范，了解他们的 JavaScript 是如何格式化的。

* [阅读地址](https://contribute.jquery.org/style-guide/js/) 

## 参考资料

* [JavaScript Standard Style官方文档](https://github.com/standard/standard/blob/master/docs/RULES-zhcn.md)
* [我为什么使用JavaScript Standard Style](http://www.css88.com/archives/7600)
* [JavaScript Standard Style（JavaScript标准编码风格）（一）](https://blog.csdn.net/henouren/article/details/77961753)
* [JavaScript Standard Style Readme](https://standardjs.com/readme-zhcn.html)
* [JavaScript Standard Style细则](https://standardjs.com/rules-zhcn.html)
* [5个JavaScript编码规范-包括AirBnB, GitHub 和 Google](http://www.css88.com/archives/8405)