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
