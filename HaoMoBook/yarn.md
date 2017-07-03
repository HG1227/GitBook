facebook开源

更快、离线安装、自动生成yarn.lock文件、网络回弹、emoji表情

安装

官网下载window版ORnpm下载安装

npm install yarn-g

使用

Yarn init

Yarn add \[组件名\]--添加组件

会与NPM冲突不推荐使用\(Yarn global add\[组件名\]--全局安装组件\)

Yarn add \[组件名\]--offline --离线安装组件

Yarn upgrade \[组件名\]--升级组件

Yarn remove \[组件名\]--删除组件

一、初识Yarn

`npm install`===`yarn`—— install 安装是默认行为。

`npm install taco --save`===`yarn add taco`—— taco 包立即被保存到 package.json 中

`npm uninstall taco --save`===`yarn remove taco`

在 npm 中，可以使用`npm config set save true`设置 —`-save`为默认行为，但这对多数开发者而言并非显而易见的。在 yarn 中，在package.json 中添加（add）和移除（remove）等行为是默认的。

`npm install taco --save-dev`===`yarn add taco --dev`

`npm update --save`===`yarn upgrade`——update（更新） vs upgrade（升级）， 赞！upgrade 才是实际做的事！版本号提升时，发生的正是upgrade！

**注意：**npm update --save 在版本 3.11 中似乎有点问题。

`npm install`[`taco@latest`](mailto:taco@latest)`--save`===`yarn add taco`

`npm install taco --global`===`yarn global add taco`—— 一如既往，请谨慎使用 global 标记。

[http://www.jb51.net/article/95199.htm](http://www.jb51.net/article/95199.htm)

NPM与yarn对照

[http://blog.csdn.net/guoquanyou/article/details/61199935](http://blog.csdn.net/guoquanyou/article/details/61199935)

二、NPM-Yarn对照列表

`npm init`===`yarn init`

`npm link`===`yarn link`

`npm outdated`===`yarn outdated`

`npm publish`===`yarn publish`

`npm run`===`yarn run`

`npm cache clean`===`yarn cache clean`

`npm login`===`yarn login`\(logout 同理\)

`npm test`===`yarn test`



# yarn {#yarn}

## 第一章 简介 {#第一章-简介}

2016年10月11日，Facebook将Yarn包管理器开源在了github上，在github上得到了很高的关注度，短短半年内github的star超过了2万多。

## 第二章 优势 {#第二章-优势}

### 2-1 极速 {#2-1-极速}

Yarn 缓存它下载的每个包，所以无需重复下载。它还并行化操作以最大化资源利用，所以安装时间比以往快。

### 2-2 超级安全 {#2-2-超级安全}

Yarn 在每个安装包的代码执行前使用校验码验证包的完整性。

### 2-3 超级可靠 {#2-3-超级可靠}

Yarn 使用一个格式详尽但简洁的 lockfile 和一个精确的算法来安装，能够保证在一个系统上的运行的安装过程也会以同样的方式运行在其他系统上。

## 第三章 安装 {#第三章-安装}

### 3-1 macOS下安装 {#3-1-macos下安装}

你可以通过 Homebrew 包管理器安装 Yarn，如果没有安装 Node.js 它也可以安装\(需要安装node.js\)。![](https://hxgqh.gitbooks.io/haomotraining/content/assets/00004.png)

### 3-2 windows下安装 {#3-2-windows下安装}

你需要在这里下载安装包\(需要安装node.js\)[https://yarnpkg.com/zh-Hans/docs/install\#windows-tab](https://yarnpkg.com/zh-Hans/docs/install#windows-tab)

### 3-3 通用的方法 {#3-3-通用的方法}

![](https://hxgqh.gitbooks.io/haomotraining/content/assets/00006.png)可以使用一下命令行查看Yarn是否安装![](https://hxgqh.gitbooks.io/haomotraining/content/assets/00007.png)

## 第四章 使用 {#第四章-使用}

### 4-1 开始新项目 {#4-1-开始新项目}

![](https://hxgqh.gitbooks.io/haomotraining/content/assets/00008.png)

### 4-2 添加依赖包 {#4-2-添加依赖包}

![](https://hxgqh.gitbooks.io/haomotraining/content/assets/00009.png)

### 4-3 升级依赖包 {#4-3-升级依赖包}

![](https://hxgqh.gitbooks.io/haomotraining/content/assets/00010.png)

### 4-4 移除依赖包 {#4-4-移除依赖包}

![](https://hxgqh.gitbooks.io/haomotraining/content/assets/00011.png)

