# Vue中使用TypeScript

#### 作者：高天阳
#### 邮箱：13683265113@163.com

```
更改历史

* 2019-07-24	    高天阳	初始化文档

```

## Vue项目中应用Typescript

> Vue CLI在2.5版本之后内置了TypeScript的支持，并且@vue/cli3提供了TypeScript插件，因此搭建支持TypeScript的vue工程非常方便

### 创建工程

```bash
npm install -g @vue/cli
```

node环境要求在8及以上 window系统不支持通过命令行 需要下载安装包进行升级

```bash
vue create project-name
```

### 添加Typescript 插件

为工程添加TypeScript插件，进入工程目录

```bash
vue add typescript
// 执行该指令后 会在项目目录中修改、或添加ts文件
```

添加成功后，我们来看下工程结构,插件已将.js文件修改成了.ts

注意：typescript 不适合在已有项目上运行，因为其特殊的语法

![](../assets/TypeScript/addTypescript.jpg)

vue-cli-plugin-typescript插件除了添加了typescript相关依赖之外，我们需要关注下vue-class-component和vue-property-decorator，
这两者是VUE的装饰器，vue-property-decorator依赖vue-class-component，class-style模式下开发时可使代码更加简明、可读，
接下来我们会举例介绍怎样更高效、优雅的书写Vue代码

### 使用Ts开发Vue

完整的Vue页面代码

> 注意：scrpit中需要指明lang=ts，否则编辑器将不能识别语言类型而报错。

```
<template>
  <div class="content-wrapper" >

  </div>
</template>

<script lang = "ts" >
	import { Component, Vue } from "vue-property-decorator";
	@Component({})
	export default class Foo extends Vue {

	}
</script>

<style scoped >
</style>
```

##### 声明响应式属性 data

```typescript
export default class App extends Vue {
  private name: string = 'kaelyn';   // 声明响应式属性
}
```

这样的写法等同于之前的

```typescript
export default {
  name: 'App',
  data() {
    return {
      name: 'kaelyn'
    }
  }
}
```

计算属性

```typescript
import { Component, Vue } from 'vue-property-decorator';
@Component({})
export default class App extends Vue {
  private number: number = 0;

  get age(): string {   // 计算属性的get
    return `I am ${this.number} years old`;
  }
  set age(value) {      // 计算属性的set
    this.number = Number(value);
  }
}
```

这样的写法等于之前的：

```
computed: {
  age: {
    get: function () {
      return `I am ${this.number} years old`;
    },
    set: function (value) {
      this.number = Number(value);
    }
  }
}
```

#### 添加vue-router

执行 ` npm i vue-router `  命令添加VueRoter，src下创建router目录、router下创建index.ts文件：

```javascript
import Vue from 'vue'
import Router from 'vue-router'
import User from '../views/User.vue'

Vue.use(Router);

const routes = [
    {
        path: '/',
        component: User
    }
];

const route = new Router({
    mode: 'history',
    routes
});

/* 前置导航守卫 */
route.beforeEach((to, from, next) => {
    // do something before next route
    next()
});

/* 后置导航守卫 */
route.afterEach((to, from) => {
    // do something after route
});

export default route
```

main.ts中加入路由：

```javascript
import Vue from 'vue'
import App from './App.vue'
import router from './router'

Vue.config.productionTip = false;

new Vue({
  render: h => h(App),
    router
}).$mount('#app');

```

### 3.2 创建User.vue

src目录下创建views目录，views下创建User.vue：

```
<template>
    <div>
        name: <input title="name" v-model="name"/><br/>
        age: <input title="age" type="number" v-model="age"/><br/>

        <button type="button" @click="onShowHelloClick">Show Hello</button>
    </div>
</template>

<script lang="ts">
    import { Component, Vue } from 'vue-property-decorator';

    @Component
    export default class User extends Vue {
        showHello = false;
        name: string = '';
        age: number = 0;

        onShowHelloClick() {
            this.showHello = !this.showHello
        }
    }
</script>

<style scoped>

</style>
```

上述写法等价于

```javascript
export default {
        name: 'user',
        data () {
            return {
                showHello: false,
                name: '',
                age: 0
            }
        },
        methods: {
            onShowHelloClick () {
                this.showHello = !this.showHello
            }
        }
    }
```

### 3.3 components、props、watch和计算属性

src/components下创建HelloWorld.vue：

```
<template>
  <div>
    {{hello}}
  </div>
</template>

<script lang="ts">
import {Component, Prop, Vue, Watch} from 'vue-property-decorator';

@Component
export default class HelloWorld extends Vue {
    @Prop({
        type: String,
        required: false,
        default: 'world'
    })
    name!: string;
    @Prop([String,Number])
    age!: number;

    helloName: string = this.name;
    helloAge: number = this.getAgeSync(this.age);

    get hello (): string {
        return `name is: ${this.name}, age is: ${this.age}`
    }

    @Watch('helloName')
    onNameChange(newVal: string, oldVal: string) {
        // do something
    }

    getAgeSync(age: number) :number {
        setTimeout(() => {}, 2000);
        return 10;
    }

}
</script>

<style scoped>

</style>
```

@Prop修饰器声明class属性为vue组件的prop；@Watch声明函数为vue的观察器；函数前添加关键字get，表明该函数为vue的计算属性。以上代码等价于

```
<script>
export default {
    name: 'HelloWorld',
    props: {
        name: {
            type: string, required: false, default: 'world'
        },
        age: {
            type: [string, number]
        }
    },
    data () {
        return {
            helloName: '',
            helloAge: 0
        }
    },
    computed: {
        hello () {
            return `name is: ${this.name}, age is: ${this.age}`
        }
    },
    watch: {
        helloName (newVal, oldVal) {
            // do something
        }
    },
    mounted () {
        this.helloName = this.name
        this.helloAge = this.getAgeSync(this.age)
    },
    methods: {
        getAgeSync(age) {
            setTimeout(() => {}, 2000)
            return 10
        }
    }
}
</script>
```

真是没有对比就没有伤害呀，不管是从语义还是代码量来讲，基于TS的声名式开发值得入坑（ps：这种声明式的语法与Java中的AT标签很相似）。

修改User.vue，使用HelloWorld组件:

```
<template>
    <div>
        name: <input title="name" v-model="name"/><br/>
        age: <input title="age" type="number" v-model="age"/><br/>

        <hello-world v-if="showHello" :name="name" :age="age"/>
        <button type="button" @click="onShowHelloClick">Show Hello</button>
    </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import HelloWorld from "../components/HelloWorld.vue";

@Component({
    components: {
        HelloWorld
    }
})
export default class User extends Vue {
    showHello = false;
    name: string = '';
    age: number = 0;

    onShowHelloClick() {
        this.showHello = !this.showHello
    }
 }
</script>

<style scoped>

</style>
```

@Component修饰器中的components参数声明了当前组件引入的外部组件。

## 参考资料

* [TypeScript 教程](https://www.runoob.com/typescript/ts-tutorial.html)
* [vue + typescript 新项目起手式](https://segmentfault.com/a/1190000011744210?utm_source=tuicool&utm_medium=referral)
* [使用 TypeScript 来写 Vue](https://blog.csdn.net/kaelyn_X/article/details/85019575)
* [!: 使用场景及问题分析](https://www.tslang.cn/docs/release-notes/typescript-2.7.html)
* [ts 新版本问题总结](https://www.jianshu.com/p/71ac8dd4c46e)
* [计算属性](https://blog.csdn.net/xlelou/article/details/81477391)
* [console报错 eslint](https://blog.csdn.net/weixin_42476786/article/details/85132793)
* [tslint 或者eslint怎样覆盖配置](https://segmentfault.com/q/1010000008691654)
* [ESlint中console.log报错问题](https://blog.csdn.net/weixin_34403976/article/details/89469152)
* [@Component修饰器相关参数和使用官方说明](https://github.com/vuejs/vue-class-component)
* [vue 修饰器vue-property-decorator官方说明](https://github.com/kaorun343/vue-property-decorator)
