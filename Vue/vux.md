# Vux使用

#### 作者：高天阳
#### 邮箱：13683265113@163.com

```
更改历史

* 2018-10-15        高天阳     初始化文档

```

## 1 简介

`VUX`（读音`[v’ju:z]`，同`views`）是基于`WeUI`和`Vue`(2.x)开发的移动端UI组件库，主要服务于微信页面。

基于`webpack + vue-loader + vux`可以快速开发移动端页面，配合`vux-loader`方便你在`WeUI`的基础上定制需要的样式。

`vux-loader`保证了组件按需使用，因此不用担心最终打包了整个vux的组件库代码。

`VUX`并不完全依赖于`WeUI`，`VUX`在`WeUI`的基础上扩展了多个常用组件，但是尽量保持整体UI样式接近`WeUI`的设计规范。

> VUX 并不是一个能解决所有场景的完美解决方案(实际上也没有一个方案能解决所有问题)，也会出现某些`bug`或者某些特性不支持，
所以如果遇到问题麻烦及时不带情绪正确反馈，我们乐于及时解决描述详细方便重现的问题。
> 
> 即使你不直接使用`VUX`组件代码, 你依然可以参考`VUX`代码来实现自己的组件库。如果一定程度上帮助到了你，那么维护这个项目也就有所意义。

#### 提示

> VUX 是库而非框架，虽然有专用的 vux-loader，但并不影响你自由地使用其他组件库或者工具库。
> 
> VUX 使用的 CSS 预处理工具是 less(同 WeUI)，但(利益于 .vue 单文件组件的灵活性)这并不影响你使用 SASS 等其他预处理器。
> 
> 用以表示该组件库时请使用大写名字 VUX，用在说明版本号时使用小写 vux@2.x。

### 1.1 在使用Vux之前

> 如果你刚从后端转到前端，可能会被目前前端(表面的)工程复杂度惊吓到，但是放心，使用`vue-cli`从模板创建项目可以快速开始编码、构建，
仅仅是几行简单的命令不是么？

在使用VUX之前需要你至少已经会使用`Vue`，同时需要你大概了解`Node.js`，`npm`，`cnpm`，`yarn`这些东西。

> 建议`Node.js`版本在`7.6.0`以上。

#### 相关工具

------

#### WeUI

VUX样式基于[`WeUI`](https://github.com/Tencent/weui)，但是你不必通过使用VUX来使用`WeUI`。
简单的页面你可以直接引入`WeUI`样式。详细请参考[`WeUI 文档`](https://github.com/Tencent/weui)。

#### Vue

VUX基于`Vue`的组件库，意味着你需要有`Vue`的基础知识。

如果还没有了解过，建议先看看[Vue官方文档](https://cn.vuejs.org/)。

#### Webpack

如果你直接使用`vux2`模板，你可以暂时不用了解。当你需要自定义一些配置时自然就能很快了解了。

[Webpack 文档](https://webpack.js.org/)

#### vue-cli

Vue 官方用于快速创建项目的工具。

```
npm install vue-cli -g
```

或者使用 yarn

```
yarn global add vue-cli
```

[vue-cli 文档](https://github.com/vuejs/vue-cli)

#### vue-loader

webpack loader，用于编译`.vue`文件，官方模板已经帮你配置好。

[vue-loader 文档](https://vue-loader.vuejs.org/)

#### vux-loader

VUX组件库的webpack loader，实现按需加载等功能。它不是替代`vue-loader`而是配合`vue-loader`使用。
如果你使用vux2模板，暂不需要手动使用它。

### 1.2 现状

### 1.3 发展

### 1.4 特点

## 2 安装和使用

### 2.1 安装

### 2.2 使用

## 3 最佳实践

### 3.1 

## 4 同类型技术比较

## 参考资料

* [router配置位置](https://www.cnblogs.com/padding1015/p/7884861.html)
* [tabber切换图标及颜色](https://blog.csdn.net/wandoumm/article/details/80168445)
* [打包报错处理：Failed to load resource: net::ERR_FILE_NOT_FOUND](https://blog.csdn.net/lhb_11/article/details/79455015)
* [x-header、tabbar固定位置](https://github.com/airyland/vux/issues/285)
* [下拉加载更多](https://www.jb51.net/article/132455.htm)
* [运行警告处理：warning：component lists rendered with v-for should have explicit keys](https://blog.csdn.net/twinkle2star/article/details/73741120)
* [Vue下路由History模式打包后页面空白](https://blog.csdn.net/sky2714/article/details/80887081)
* [scroller下拉失败回弹](https://blog.csdn.net/hh_liweihong/article/details/77066023)
* [打包后css引用图片资源找不到](https://blog.csdn.net/gdut_luoyifei/article/details/79001397)
* [打包后js引用图片资源找不到](https://blog.csdn.net/github_37533433/article/details/78937645)
* [上传图片组件](https://www.npmjs.com/package/vux-uploader)
* [上传图片组件引入报错](https://blog.csdn.net/wandoumm/article/details/80167708)
* [报错处理：exports is not defined](https://segmentfault.com/q/1010000011817644/a-1020000011818193)
* [报错处理：Default export is not declared in imported module](https://segmentfault.com/q/1010000004664827)
* 上一个问题可参考yumaomoney_WeChat/src/components/container/Container.vue，export default为必要内容。
* [vux中fullpage的使用](https://www.jb51.net/article/108893.htm)
* VChart异步加载表格数据时，tooltip在初始化、请求后需要渲染两次，否则无法加载具体比例。
* [Vue Router 的params和query传参的使用和区别](https://blog.csdn.net/mf_717714/article/details/81945218)
* [vux框架组件自定义样式](https://blog.csdn.net/linggty/article/details/81512211)
