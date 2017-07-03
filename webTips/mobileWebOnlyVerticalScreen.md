## 通过css媒体查询来判断，当横屏时，弹出相应提示。

```
@media all and (orientation : landscape) {
    /*横屏时代码*/
}

@media all and (orientation : portrait){
    /*竖屏时代码*/
}
```

## 浏览器自带属性

```
<!-- UC强制竖屏 -->
<meta name="screen-orientation" content="portrait">

<!-- QQ强制竖屏 -->
<meta name="x5-orientation" content="portrait">

<!-- UC强制全屏 -->
<meta name="full-screen" content="yes">

<!-- QQ强制全屏 -->
<meta name="x5-fullscreen" content="true">

<!-- UC应用模式 -->
<meta name="browsermode" content="application">

<!-- QQ应用模式 -->
<meta name="x5-page-mode" content="app">

<!-- windows phone 点击无高光 -->
<meta name="msapplication-tap-highlight" content="no">

<!-- 适应移动端 END -->
```