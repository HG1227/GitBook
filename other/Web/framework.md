# 框架方面

#### 作者：高天阳
#### 邮箱：13683265113@163.com

```
更改历史

* 2019-08-09        高天阳     初始化文档

```

### 组件的全局引入和局部引入是怎么写的



### VUE项目的浏览器判断应该写在哪里



### VUE项目的SEO问题如何解决



### 写出符合以下规则的Vue的路由

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

### 使用Vue时，页面的加载动画适合在哪个阶段(生命周期/钩子函数)触发

