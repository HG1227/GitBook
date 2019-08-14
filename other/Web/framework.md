# 框架方面

#### 作者：高天阳
#### 邮箱：13683265113@163.com

```
更改历史

* 2019-08-09        高天阳     初始化文档

```

## vue的状态管理Vuex是什么

1. 在store下的Index.js中的state设置一个属性
2. 在所需的a页面把需要的数据存入commit:自定义名字为updateUserdata
3. 回到index.js页面修改属性:修改属性时传入的obj对象后所带属性名必须和commit中定义的为一致,之后再赋给设置属性

## 组件的全局引入和局部引入是怎么写的

全局组件引入写法：在项目的main.js中：

```javascript
import Vue from 'vue';
import MyComponent from '@/components/MyComponent.vue'; // 导入自己写的组件文件
 
Vue.use(MyComponent); // 自定义全局组件的时候需要Vue.use();
 
Vue.component('my-component', MyComponent); //初始化组件
 
new Vue({
  el: '#app',
  router,
  components: {
    App,
    MyComponent
  },
  template: '<App/>',
});
```

局部组件引入写法：在需要使用组件的a.vue文件中：

```
<template>
</template>
 
<script>
import MyComponent from '@/components/MyComponent.vue';
export default {
  components: {MyComponent}, // 直接初始化就可以啦，不需要Vue.use();
  data() {},
  methods: {}
};
</script>
 
<style lang="scss" scoped>
</style>
```

下面附上自定义组件的MyComponent.vue文件代码：

```
<template>
  <div>
    <a @click="methods1()"></a>
  </div>
</template>
<script>
import { MessageBox } from 'mint-ui';
export default {
  data () { // 组件内参数定义在data中
    return {
      data1: {}
    };
  },
  props: { // 组件传参使用props
    value1: String,
    value2: Number
  },
  methods: { // 组件的计算方法
    methods1 () {
    }
  }
};
</script>
<style lang="scss" scoped>
</style>
```

## 引入插件时vue.use和vue.prototype的区别

1. 不是为了vue写的插件(插件内要处理)不支持vue.use()加载方式
1. 非vue官方库不支持new vue()方式
1. 每一个vue组件都是vue实例，所以组件内this可以拿到vue.prototype上添加的属性和方法

## vue如何声明全局变量、方法

1. 定义全局变量模块文件 Global.vue 并将其中的变量暴露出去
2. 在需要使用的模块进行调用
3. 在main.js文件引入全局变量模块 并挂在在Vue.prototype
4. 微信项目中 挂载了一些数据json 以及随机color库等
5. 公共方法如增删改查方法的提炼 或 不同页面弹出框调用方法

## 组件之间的通讯

1. 父传子 通过props属性 props除了接受数据 还可以定义数据类型 是否必传 逻辑处理等
2. 子传父 通过$emit自定义方法，将数据传递到父页面
3. 兄弟传参 通过空的vue实例作为中转站

## VUE项目的浏览器判断应该写在哪里



## VUE项目的SEO问题如何解决

SEO及网站渲染

1. 后端渲染: 指传统的 ASP、Java 或 PHP 的渲染机制；
    1. 好处: 前端耗时少（前端只负责将html进行展示），利于SEO
    1. 坏处: 网络传输数据量大，占用（部分、少部分）服务器运算资源，response 出的数据量会（稍）大点，模板改了前端的交互和样式什么的一样得跟着联动修改。
1. 前端渲染: 指使用 JS 来渲染页面大部分内容，代表是现在流行的 SPA 单页面应用；
    1. 好处: 
        1. 局部刷新。无需每次都进行完整页面请求
        1. 懒加载。如在页面初始时只加载可视区域内的数据，滚动后rp加载其它数据，可以通过 react-lazyload 实现
        1. 富交互。使用 JS 实现各种酷炫效果
        1. 节约服务器成本。省电省钱，JS 支持 CDN 部署，且部署极其简单，只需要服务器支持静态文件即可
        1. 天生的关注分离设计。服务器来访问数据库提供接口，JS 只关注数据获取和展现
        1. JS 一次学习，到处使用。可以用来开发 Web、Serve、Mobile、Desktop 类型的应用
    1. 坏处: 前端耗时较多，不利于SEO，首屏加载慢。
    
vue-cli3解决SEO以及首屏加载问题

1.vue ssr

优点：

更好的SEO，由于搜索引擎爬虫抓取工具可以直接查看完全渲染的页面。更快的内容到达时间(time-to-content)，
特别是对于缓慢的网络情况或运行缓慢的设备。

缺点：

1. 浏览器特定的代码，只能在某些生命周期钩子函数(lifecycle hook)中使用；一些外部扩展库(external library)可能需要特殊
处理，才能在服务器渲染应用程序中运行。
1. 涉及构建设置和部署的更多要求。
1. 更多的服务器端负载。

2.nuxt.js

Nuxt 是一个基于 Vue 生态的更高层的框架，为开发服务端渲染的 Vue 应用提供了极其便利的开发体验。
甚至可以用它来做为静态站生成器。比ssr更加简单亲民

3.预渲染：prerender-spa-plugin插件

如果只是改善少数营销页面（例如 /, /about, /contact 等）的 SEO，那么你可能需要预渲染。
无需使用 web 服务器实时动态编译 HTML，而是使用预渲染方式，在构建时(build time)简单地生成针对特定路由的静态 HTML 文件。
优点是设置预渲染更简单，并可以将你的前端作为一个完全静态的站点。

[VUE项目SEO问题的解决](https://blog.csdn.net/MiemieWan/article/details/84976052)

## 写Vue的路由vue-router

1. vue-router配置 path：’url’ 、name：’名称’、 component：‘模块引入’ 、children：‘子模块’ 
2. 注意配置带子模块时 自身的模块引入需要是一个空的 container
3. hash和history的差异
    1. hash是标准格式 带# 不是很美观
    2. history更像一个应用 没有# 但是不能设置在非项目根目录下 (文件的资源会找不到 通过配置可以 但还有兼容问题 安卓微信浏览器被404劫持 遂弃用history)
4. vue-router有哪些钩子
    1. beforeEach 判断登录状态
    2. afterEach 页面回滚置顶

## 写出符合以下规则的Vue的路由

```javascript
{
    noticesIndex: '/notices'
    noticesIndex: '/notices/platform/{任意字母}/type/{任意数字}'
    noticesDetails: '/notices/{任意32位字符数字组合}'
}
vuerouter = [
    {
        path:'/notices/platform/:str(\[A-Za-z]+)/type/:num(\\d+)',
        name:'noticseIndex',
        component:NoticesIndex
    },
    {
        path:'/notices/:str(^[a-zA-Z0-9]{32}$)',
        name:'noticesDetails',
        component:NoticesIndex
    }
]
```

[vue-router高级匹配模式](https://router.vuejs.org/zh/guide/essentials/dynamic-matching.html#%E6%8D%95%E8%8E%B7%E6%89%80%E6%9C%89%E8%B7%AF%E7%94%B1%E6%88%96-404-not-found-%E8%B7%AF%E7%94%B1)
[vue-router高级匹配模式文档](https://github.com/vuejs/vue-router/blob/dev/examples/route-matching/app.js)

## 使用Vue时，页面的加载动画适合在哪个阶段(生命周期/钩子函数)触发

均用到了`<transition>`标签

方式一：css动画

方式二：使用animate.css动画库

方式三：使用Js钩子函数

方式四：使用velocity js动画库

[vue中动画的实现的几种方式](https://www.jianshu.com/p/5c34fafd22da)
[vue官方文档过渡 & 动画](https://cn.vuejs.org/v2/guide/transitions.html)

## Vue的自定义指令

1. 自定义指令跟过滤器非常相似 单就定义方式而言 其与过滤器完全一致 分为局部指令 和全局指令 不过就是filter改为directive的区别
2. 使用场景
    1. 对dom的操作 例如滑动切换 图片未加载时的背景色
    2. 第三方插件的集成
3. 钩子函数
    1. bind(常用): 只调用一次，指令第一次绑定到元素时调用，用这个钩子函数可以定义一个在绑定时执行一次的初始化动作
    2. inserted(常用): 被绑定元素插入父节点时调用（父节点存在即可调用，不必存在于 document 中）
    3. update: 被绑定元素所在的模板更新时调用，而不论绑定值是否变化。通过比较更新前后的绑定值，可以忽略不必要的模板更新（详细的钩子函数参数见下）
    4. componentUpdated: 被绑定元素所在模板完成一次更新周期时调用
    5. unbind: 只调用一次， 指令与元素解绑时调用

