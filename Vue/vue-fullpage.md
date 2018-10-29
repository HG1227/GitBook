# vue-fullpage使用

#### 作者：高天阳
#### 邮箱：13683265113@163.com

```
更改历史

* 2018-10-29        高天阳     初始化文档

```

## 1 简介

可实现移动端的单页滚动效果，支持横向滚动和纵向滚动

> 兼容性

目前还未进行大规模兼容性测试。有bug请提问至issues

## 2 安装

```
npm install vue-fullpage --save
```

`commonjs`

```
import VueFullpage from 'vue-fullpage'
Vue.use(VueFullpage)
```

或

```
var vueFullpage = require('vue-fullpage')
Vue.use(vueFullpage)
```

## 3 快速上手

模板部分：在`page-container`容器加入`v-cover`指令防止闪烁在`page-wp`容器上加`v-page`指令，指令值是`fullpage`的配置

```
<div class="page-container">
    <div v-page="opts" class="page-wp">
        <div class="page page1">
            <p class="part part1" v-animate="'slideIn'">
            vue-fullpage
            </p>
        </div>
        <div class="page page2">
            <p class="part part2" v-animate="'slideIn'">
            vue-fullpage
            </p>
        </div>
        <div class="page page3">
            <p class="part part3" v-animate="'slideIn'">
            vue-fullpage
            </p>
        </div>
        <div class="page page4">
            <p class="part part4" v-animate="'fadeIn'">
            vue-fullpage
            </p>
        </div>
    </div>
</div>
```

js部分：提供 vue-fullpage 的自定义指令

```
<script>
export default {
    data () {
        return {
            opts: {
                start: 0,
                dir: 'v',
                loop: false,
                duration: 500,
                stopPageScroll: true,
                beforeChange: function (prev, next) {
                },
                afterChange: function (prev, next) {
                }
            }
        }
    }
}
</script>
```

css部分： page-container 需要固定宽度和高度， fullpage 会使用父元素的宽度和高度。

如下设置可使滚动页面充满全屏

```
<style>
    .page-container {
        position: absolute;
        left: 0;
        top: 0;
        width: 100%;
        height: 100%;
    }
</style>
```

[demo地址](http://vue.wendaosanshou.top/vue_fullpage_demo/)

* 注意:VChart异步加载表格数据时，tooltip在初始化、请求后需要渲染两次，否则无法加载具体比例。

## 参考资料

* [vux中fullpage的使用](https://www.jb51.net/article/108893.htm)
