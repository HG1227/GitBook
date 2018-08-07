# Vue的Ref属性

#### 作者：高天阳
#### 邮箱：13683265113@163.com

```
更改历史

* 2018-8-7	    高天阳	初始化文档

```

## 1 Vue的ref和$refs属性

### 1.1 简介

`ref`被用来给DOM元素或子组件注册引用信息。引用信息会根据父组件的`$refs`对象进行注册。
如果在普通的DOM元素上使用，引用信息就是元素; 如果用在子组件上，引用信息就是组件实例

* 注意：只要想要在Vue中直接操作DOM元素，就必须用ref属性进行注册

```
<!-- vm.$refs.p will the DOM node -->
<p ref='p'>hello</p>

<!-- vm.$refs.child will be child comp instance -->
<child-comp ref='child'></child-comp>
```

示例：

```
<div class="goods">
    <div class="menu-wrapper" ref="menuWrapper">
        <ul>
            <li v-for="item in goods" class="menu-item">
                <span class="text border-1px">
                    <span v-show="item.type>0" class="icon" v-bind:class="classMain">
                        {{item.name}}
                    </span>
                </span>
            </li>
        </ul>
    </div>
</div>
<div class="foods-wrapper" ref="foodsWrapper">
    <ul>
        <li v-for="item in goods" class="food-list"></li>
    </ul>
</div>
```

```
created: function () {
    var self = this;
    self.$http.get('/api/goods').then((res) => {
        self.goods = res.body.dataJson;
        // 这里获取数据赋予data中的goods属性，进而去更新视图层的展示，但因为Vue中更新DOM是异步的，所以这里即使更新goods也不会立刻改变DOM，所以我们必须使用nextTick的API操作DOM
        self.$nextTick(() => {
            self._initScroll();
        })
    });
    self.classMap = ['decrease','discount','guarantee','invoice','special'];
},
methods: {
    /**
     * 初始化
     */
    _initScroll() {
        var self = this;
        self.foodsScroll = new BScroll(self.$refs.foodsWrapper,{})
        self.menuScroll = new BScroll(self.$refs.menuWrapper,{})
    }
}
```

这里为了在create的时候引用DOM元素，先在DOM中使用ref标签进行了注册，然后便可以通过’this.$refs’再跟注册时的名称来引用DOM元素了

## 2 vue中的ref和$refs

## 2.1 vm.$refs

* 类型:`Object`
* 只读
* 详细:

一个对象，持有已注册过的`ref`[特性](https://cn.vuejs.org/v2/api/#ref)的所有子组件

* 参考：

    * [子组件引用](https://cn.vuejs.org/v2/guide/components.html#%E5%8A%A8%E6%80%81%E7%BB%84%E4%BB%B6)
    * [特殊特性 - ref](https://cn.vuejs.org/v2/api/#ref)

### 2.2 ref

* 预期:`string`

`ref`被用来给元素或子组件注册引用信息。引用信息将会注册在父组件的`$refs`对象上。如果在普通的 DOM 元素上使用，
引用指向的就是 DOM 元素；如果用在子组件上，引用就指向组件实例：

```
<!-- vm.$refs.p will the DOM node -->
<p ref='p'>hello</p>

<!-- vm.$refs.child will be child comp instance -->
<child-comp ref='child'></child-comp>
```

当 `v-for` 用于元素或组件的时候，引用信息将是包含 DOM 节点或组件实例的数组。

关于 `ref` 注册时间的重要说明：因为 `ref` 本身是作为渲染结果被创建的，在初始渲染的时候你不能访问它们 - 它们还不存在！
`$refs` 也不是响应式的，因此你不应该试图用它在模板中做数据绑定。

* 参考：子组件 [子组件Refs](https://cn.vuejs.org/v2/guide/components.html#%E5%8A%A8%E6%80%81%E7%BB%84%E4%BB%B6)

## 3 ref的使用实例