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

