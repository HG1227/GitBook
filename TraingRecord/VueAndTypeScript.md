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

vue-cli-plugin-typescript插件除了添加了typescript相关依赖之外，我们需要关注下vue-class-component和vue-property-decorator，
这两者是VUE的装饰器，vue-property-decorator依赖vue-class-component，class-style模式下开发时可使代码更加简明、可读，
接下来我们会举例介绍怎样更高效、优雅的书写Vue代码

### 使用Ts开发Vue

完整的Vue页面代码

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

```javascript
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
