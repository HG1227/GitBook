# clipboard使用

#### 作者：高天阳
#### 邮箱：13683265113@163.com

```
更改历史

* 2018-10-29        高天阳     初始化文档

```

## 1 简介

clipboard.js用来实现vue实现复制到粘贴板功能

## 2 安装
  
* 注意:出现错误的话，可以试试`cnpm`

```
npm install --save vue-clipboard2
```

## 3 使用

对于vue-cli

```
import Vue from 'vue'
import VueClipboard from 'vue-clipboard2'
```

对于常规的用法

```
<script src="vue.min.js"></script>
<!-- 必须在vue.js之后放置这一行 -->
<script src="vue-clipboard.min.js"></script>
```

## 4 示例

```
<template>
  <div class="wxsmallcode-page publicCon">
    <div class="copyBox">
      sysAppId：<span>{{sysAppIds}}</span>
      <el-button class="ml10" type="text" size="medium"
        v-clipboard:copy="sysAppIds"
        v-clipboard:success="onCopy"
        v-clipboard:error="onError">点击复制</el-button>
    </div>
</template>
<script>
export default {
  data(){
    return {
      sysAppIds: 'xxxxxxxxxxxsx'
    }
  },
  methods: {
    // 复制成功
    onCopy(e){
      console.log(e);
    },
    // 复制失败
    onError(e){
      alert("失败");
    },
  }
}
</script>
```

* 注：cnpm 为安装了淘宝镜像之后的命令工具

## 参考资料

* [clipboard.js复制至剪贴板插件](https://www.cnblogs.com/wyhlightstar/p/8950430.html)