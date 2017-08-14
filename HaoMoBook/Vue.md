# Vue.js

## 第一章 介绍

### 1.1 Vue.js 是什么

Vue.js（读音 /vjuː/，类似于view） 是一套构建用户界面的渐进式框架。与其他重量级框架不同的是，Vue 采用自底向上增量开发的设计。Vue 的核心库只关注视图层，它不仅易于上手，还便于与第三方库或既有项目整合。另一方面，当与单文件组件和Vue 生态系统支持的库结合使用时，Vue 也完全能够为复杂的单页应用程序提供驱动。
如果你是有经验的前端开发者，想知道 Vue.js 与其它库/框架的区别，查看对比其它框架。

## 第二章 安装

### 2.1 兼容性

Vue.js 不支持 IE8 及其以下版本，因为 Vue.js 使用了 IE8 不能模拟的 ECMAScript 5 特性。 Vue.js 支持所有
兼容 ECMAScript 5 的浏览器。

### 2.2 安装

1.直接下载并用`<script>`标签引入，Vue会被注册为一个全局变量。
重要提示：在开发时请用开发版本，遇到常见错误它会给出友好的警告。
2.在用 Vue.js 构建大型应用时推荐使用 NPM 安装， NPM 能很好地和诸如Webpack或Browserify模块打包器配合使用。 Vue.js 也提供配套工具来开发单文件组件。

#### 最新稳定版
```angular2html
$ npm install vue
Bower 只提供 UMD 构建。
```
#### 最新稳定版本
```
$ bower install vue
```

### 2.3 命令行工具

Vue.js 提供一个官方命令行工具，可用于快速搭建大型单页应用。该工具提供开箱即用的构建工具配置，带来现代化的前端开发流程。只需几分钟即可创建并启动一个带热重载、保存时静态检查以及可用于生产环境的构建配置的项目：

* 全局安装 vue-cli
```angular2html
$ npm install --global vue-cli
```
* 创建一个基于 webpack 模板的新项目
```angular2html
$ vue init webpack my-project
```
* 安装依赖，走你
```angular2html
$ cd my-project
$ npm install
$ npm run dev
```
## 第三章 内置指令

#### 1.v-text
预期：string
详细：

更新元素的textContent。如果要更新部分的textContent，需要使用``插值。
示例：

```
<spanv-text="msg"></span>
<!-- 和下面的一样 -->
<span>{{msg}}</span>
```
参考：数据绑定语法 - 插值

#### 2.v-html
预期：string
详细：

更新元素的innerHTML。注意：内容按普通 HTML 插入 - 不会作为 Vue 模板进行编译。如果试图使用v-html组合模板,可以重新考虑是否通过使用组件来替代。
在网站上动态渲染任意 HTML 是非常危险的，因为容易导致XSS 攻击。只在可信内容上使用v-html，永不用在用户提交的内容上。
示例：
```angular2html
<div v-html="html"></div>
```
参考：数据绑定语法 - 插值

#### 3.v-show
预期：any
用法：

根据表达式之真假值，切换元素的displayCSS 属性。
当条件变化时该指令触发过渡效果。
当和v-if一起使用时，v-for的优先级比v-if更高。详见列表渲染教程
参考：条件渲染 - v-show

#### 4.v-if
预期：any
用法：

根据表达式的值的真假条件渲染元素。在切换时元素及它的数据绑定 / 组件被销毁并重建。如果元素是<template>，将提出它的内容作为条件块。
当条件变化时该指令触发过渡效果。
参考：条件渲染 - v-if
v-if和v-show
v-if是“真正的”条件渲染，因为它会确保在切换过程中条件块内的事件监听器和子组件适当地被销毁和重建。
v-if也是惰性的：如果在初始渲染时条件为假，则什么也不做——直到条件第一次变为真时，才会开始渲染条件块。
相比之下，v-show就简单得多——不管初始条件是什么，元素总是会被渲染，并且只是简单地基于 CSS 进行切换。
一般来说，v-if有更高的切换开销，而v-show有更高的初始渲染开销。因此，如果需要非常频繁地切换，则使用v-show较好；如果在运行时条件不太可能改变，则使用v-if较好。

#### 5.v-else
不需要表达式
限制：前一兄弟元素必须有v-if或v-else-if。
用法：

为v-if或者v-else-if添加 “else 块”。
    <div v-if="Math.random() > 0.5">
      Now you see me
    </div>
    <div v-else>
      Now you don't
    </div>
参考：

条件渲染 - v-else

#### 6.v-else-if

### 2.1.0 新增
类型:any
限制:前一兄弟元素必须有v-if或v-else-if。
用法:

表示v-if的 “else if 块”。可以链式调用。
```angular2html
<div v-if="type === 'A'">
  A
</div>
<div v-else-if="type === 'B'">
  B
</div>
<div v-else-if="type === 'C'">
  C
</div>
<div v-else>
  Not A/B/C
</div>
```
参考:条件渲染 - v-else-if

#### 7.v-for
预期：Array | Object | number | string
用法：

基于源数据多次渲染元素或模板块。此指令之值，必须使用特定语法alias in expression，为当前遍历的元素提供别名：
```angular2html
<div v-for="item in items">
  {{ item.text }}
</div>
```
另外也可以为数组索引指定别名（或者用于对象的键）：
```angular2html
<div v-for="(item, index) in items"></div>
<div v-for="(val, key) in object"></div>
<div v-for="(val, key, index) in object"></div>
```
v-for默认行为试着不改变整体，而是替换元素。迫使其重新排序的元素,您需要提供一个key的特殊属性:
```angular2html
<div v-for="item in items" :key="item.id">
  {{ item.text }}
</div>
```
v-for的详细用法可以通过以下链接查看教程详细说明。
参考：

列表渲染
key

#### 8.v-on
缩写：@

预期：Function | Inline Statement | Object
参数：event
修饰符：

.stop
调用 event.stopPropagation() 。
.prevent
调用 event.preventDefault() 。
.capture
添加事件侦听器时使用 capture 模式。
.self
只当事件是从侦听器绑定的元素本身触发时才触发回调。
.{keyCode | keyAlias}
只当事件是从特定键触发时才触发回调。
.native
监听组件根元素的原生事件。
.once
只触发一次回调。
.left
(2.2.0) 只当点击鼠标左键时触发。
.right
(2.2.0) 只当点击鼠标右键时触发。
.middle
(2.2.0) 只当点击鼠标中键时触发。
.passive
(2.3.0) 以 { passive: true } 模式添加侦听器
用法：

绑定事件监听器。事件类型由参数指定。表达式可以是一个方法的名字或一个内联语句，如果没有修饰符也可以省略。
从2.4.0开始，v-on同样支持不带参数绑定一个事件/监听器键值对的对象。注意当使用对象语法时，是不支持任何修饰器的。
用在普通元素上时，只能监听原生 DOM 事件。用在自定义元素组件上时，也可以监听子组件触发的自定义事件。
在监听原生 DOM 事件时，方法以事件为唯一的参数。如果使用内联语句，语句可以访问一个$event属性：v-on:click="handle('ok', $event)"。
示例：
```angular2html
<!-- 方法处理器 -->
<button v-on:click="doThis"></button>
<!-- 对象语法 (2.4.0+) -->
<button v-on="{ mousedown: doThis, mouseup: doThat }"></button>
<!-- 内联语句 -->
<button v-on:click="doThat('hello', $event)"></button>
<!-- 缩写 -->
<button @click="doThis"></button>
<!-- 停止冒泡 -->
<button @click.stop="doThis"></button>
<!-- 阻止默认行为 -->
<button @click.prevent="doThis"></button>
<!-- 阻止默认行为，没有表达式 -->
<form @submit.prevent></form>
<!--  串联修饰符 -->
<button @click.stop.prevent="doThis"></button>
<!-- 键修饰符，键别名 -->
<input @keyup.enter="onEnter">
<!-- 键修饰符，键代码 -->
<input @keyup.13="onEnter">
<!-- 点击回调只会触发一次 -->
<button v-on:click.once="doThis"></button>
```

在子组件上监听自定义事件（当子组件触发 “my-event” 时将调用事件处理器）：
```angular2html
<my-component @my-event="handleThis"></my-component>
<!-- 内联语句 -->
<my-component @my-event="handleThis(123, $event)"></my-component>
<!-- 组件中的原生事件 -->
<my-component @click.native="onClick"></my-component>
```

参考：

方法与事件处理器
组件 - 自定义事件

#### 9.v-bind
缩写：:

预期：any (with argument) | Object (without argument)
参数：attrOrProp (optional)
修饰符：

.prop
被用于绑定 DOM 属性。( what’s the difference? )
.camel
(2.1.0+) 将 kebab-case 特性名转换为 camelCase. (从 2.1.0 开始支持)
.sync (2.3.0+) 语法糖，会扩展成一个更新父组件绑定值的 v-on 侦听器。
用法：

动态地绑定一个或多个特性，或一个组件 prop 到表达式。
在绑定class或style特性时，支持其它类型的值，如数组或对象。可以通过下面的教程链接查看详情。
在绑定 prop 时，prop 必须在子组件中声明。可以用修饰符指定不同的绑定类型。
没有参数时，可以绑定到一个包含键值对的对象。注意此时class和style绑定不支持数组和对象。
示例：

```
<!-- 绑定一个属性 -->
<img v-bind:src="imageSrc">
<!-- 缩写 -->
<img :src="imageSrc">
<!-- 内联字符串拼接 -->
<img :src="'/path/to/images/' + fileName">
<!-- class 绑定 -->
<div :class="{ red: isRed }"></div>
<div :class="[classA, classB]"></div>
<div :class="[classA, { classB: isB, classC: isC }]">
<!-- style 绑定 -->
<div :style="{ fontSize: size + 'px' }"></div>
<div :style="[styleObjectA, styleObjectB]"></div>
<!-- 绑定一个有属性的对象 -->
<div v-bind="{ id: someProp, 'other-attr': otherProp }"></div>
<!-- 通过 prop 修饰符绑定 DOM 属性 -->
<div v-bind:text-content.prop="text"></div>
<!-- prop 绑定. “prop” 必须在 my-component 中声明。 -->
<my-component :prop="someThing"></my-component>
<!-- 通过 $props 将父组件的 props 一起传给子组件 -->
<child-component v-bind="$props"></child-component>
<!-- XLink -->
<svg><a :xlink:special="foo"></a></svg>
```

.camel修饰符允许在使用 DOM 模板时将v-bind属性名称驼峰化，例如 SVG 的viewBox属性：
```angular2html
<svg :view-box.camel="viewBox"></svg>
```

在使用字符串模板或通过vue-loader/vueify编译时，无需使用.camel。
参考：

Class 与 Style 绑定
组件 - 组件 Props
组件 -.sync修饰符


#### 10.v-model
预期：随表单控件类型不同而不同。
限制：

```angular2html
<inpit></inpit>
<select></select>
<textarea></textarea>
```
components
修饰符：

.lazy
取代 input 监听 change 事件
.number
输入字符串转为数字
.trim
输入首尾空格过滤
用法：

在表单控件或者组件上创建双向绑定。细节请看下面的教程链接。
参考：

表单控件绑定
组件 - 在输入组件上使用自定义事件

#### 11.v-pre
不需要表达式
用法：

跳过这个元素和它的子元素的编译过程。可以用来显示原始 Mustache 标签。跳过大量没有指令的节点会加快编译。
示例：
```angular2html
<span v-pre>{{ "this will not be compiled" }}</span>
```

#### 12.v-cloak
不需要表达式
用法：

这个指令保持在元素上直到关联实例结束编译。和 CSS 规则如`[v-cloak]` { display: none }一起用时，这个指令可以隐藏未编译的 Mustache 标签直到实例准备完毕。
示例：

```angular2html
[v-cloak]{
  display: none;
}
<div v-cloak>
  {{ message }}
</div>
```
不会显示，直到编译结束

#### 13.v-once
不需要表达式
详细：

只渲染元素和组件一次。随后的重新渲染,元素/组件及其所有的子节点将被视为静态内容并跳过。这可以用于优化更新性能。
```angular2html
<!-- 单个元素 -->
<span v-once>This will never change: {{msg}}</span>
<!-- 有子元素 -->
<div v-once>
  <h1>comment</h1>
  <p>{{msg}}</p>
</div>
<!-- 组件 -->
<my-component v-once :comment="msg"></my-component>
<!-- v-for 指令-->
<ul>
  <li v-for="i in list" v-once>{{i}}</li>
</ul>
```
参考：

数据绑定语法- 插值
组件 - 使用 v-once 实现轻量的静态组件
第四章 自定义指令

### 4.1 简介

除了默认设置的核心指令( v-model 和 v-show ),Vue 也允许注册自定义指令。注意，在 Vue2.0 里面，代码复用的主要形式和抽象是组件——然而，有的情况下,你仍然需要对纯 DOM 元素进行底层操作,这时候就会用到自定义指令。
下面这个例子将聚焦一个 input 元素,代码如下：
```angular2html
// 注册一个全局自定义指令 v-focus
Vue.directive('focus', {
  // 当绑定元素插入到 DOM 中。
  inserted: function (el) {
    // 聚焦元素
    el.focus()
  }
})
```

然后你可以在模板中任何元素上使用新的 v-focus 属性：
<input v-focus>

### 4.2 钩子函数

指令定义函数提供了几个钩子函数（可选）：
bind: 只调用一次，指令第一次绑定到元素时调用，用这个钩子函数可以定义一个在绑定时执行一次的初始化动作。
inserted: 被绑定元素插入父节点时调用（父节点存在即可调用，不必存在于 document 中）。
update: 所在组件的 VNode 更新时调用，但是可能发生在其孩子的 VNode 更新之前。指令的值可能发生了改变也可能没有。但是你可以通过比较更新前后的值来忽略不必要的模板更新 (详细的钩子函数参数见下)。
componentUpdated: 所在组件的 VNode及其孩子的 VNode全部更新时调用。
unbind: 只调用一次， 指令与元素解绑时调用。
接下来我们来看一下钩子函数的参数 (包括el，binding，vnode，oldVnode) 。

### 4.3 钩子函数参数

钩子函数被赋予了以下参数：
el: 指令所绑定的元素，可以用来直接操作 DOM 。
binding: 一个对象，包含以下属性：
name: 指令名，不包括v-前缀。
value: 指令的绑定值， 例如：v-my-directive="1 + 1", value 的值是2。
oldValue: 指令绑定的前一个值，仅在update和componentUpdated钩子中可用。无论值是否改变都可用。
expression: 绑定值的字符串形式。 例如v-my-directive="1 + 1"， expression 的值是"1 + 1"。
arg: 传给指令的参数。例如v-my-directive:foo， arg 的值是"foo"。
modifiers: 一个包含修饰符的对象。 例如：v-my-directive.foo.bar, 修饰符对象 modifiers 的值是{ foo: true, bar: true }。
vnode: Vue 编译生成的虚拟节点，查阅VNode API了解更多详情。
oldVnode: 上一个虚拟节点，仅在update和componentUpdated钩子中可用。
样例：

```angular2html
<div id="hook-arguments-example" v-demo:foo.a.b="message"></div>
Vue.directive('demo', {
  bind: function (el, binding, vnode) {
    var s = JSON.stringify
    el.innerHTML =
      'name: '       + s(binding.name) + '<br>' +
      'argument: '   + s(binding.arg) + '<br>' +
      'modifiers: '  + s(binding.modifiers) + '<br>' +
      'vnode keys: ' + Object.keys(vnode).join(', ')
  }
})
new Vue({
  el: '#hook-arguments-example',
  data: {
    message: 'hello!'
  }
})
name: "demo"
value: "hello!"
expression: "message"
argument: "foo"
modifiers: {"a":true,"b":true}
vnode keys: tag, data, children, text, elm, ns, context, functionalContext, key, componentOptions, componentInstance, parent, raw, isStatic, isRootInsert, isComment, isCloned, isOnce, asyncFactory, asyncMeta, isAsyncPlaceholder
```

### 4.4 函数简写

大多数情况下，我们可能想在bind和update钩子上做重复动作，并且不想关心其它的钩子函数。可以这样写:
```angular2html
Vue.directive('color-swatch', function (el, binding) {
  el.style.backgroundColor = binding.value
})
```

4.5 对象自变量

如果指令需要多个值，可以传入一个 JavaScript 对象字面量。记住，指令函数能够接受所有合法类型的 JavaScript 表达式。
```angular2html
<div v-demo="{ color: 'white', text: 'hello!' }"></div>
Vue.directive('demo', function (el, binding) {
  console.log(binding.value.color) // => "white"
  console.log(binding.value.text)  // => "hello!"
})
```

## 第五章 过滤器

Vue.js 允许你自定义过滤器，可被用作一些常见的文本格式化。过滤器可以用在两个地方：mustache 插值和v-bind表达式。过滤器应该被添加在 JavaScript 表达式的尾部，由“管道”符指示：
```angular2html
<!-- in mustaches -->
{{ message | capitalize }}
<!-- in v-bind -->
<div v-bind:id="rawId | formatId"></div>
```

过滤器函数总接受表达式的值 (之前的操作链的结果) 作为第一个参数。在这个例子中，capitalize过滤器函数将会收到message
的值作为第一个参数。
```angular2html
new Vue({
  // ...
  filters: {
    capitalize: function (value) {
      if (!value) return ''
      value = value.toString()
      return value.charAt(0).toUpperCase() + value.slice(1)
    }
  }
})
```

过滤器可以串联：
```angular2html
{{ message | filterA | filterB }}
```

在这个例子中，filterA拥有单个参数，它会接收message的值，然后调用filterB，且filterA的处理结果将会作为filterB的单个参数传递进来。
过滤器是 JavaScript 函数，因此可以接受参数：
```angular2html
{{ message | filterA('arg1', arg2) }}
```

这里，filterA是个拥有三个参数的函数。message的值将会作为第一个参数传入。字符串'arg1'将作为第二个参数传给filterA，表达式arg2的值将作为第三个参数。