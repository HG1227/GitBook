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

