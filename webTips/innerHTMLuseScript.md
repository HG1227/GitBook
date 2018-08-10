# innerHTML引入的script如何使用

#### 作者：高天阳
#### 邮箱：13683265113@163.com

```
更改历史

* 2018-8-9 高天阳	初始化文档

```

## 1 问题概要

今天来简单聊聊如何让 `innerHTML` 进来的 `scrip` 代码跑起来的问题。

前台请求一个接口，接口返回一些 `HTML` 标签拼接成的字符串，以供前端直接 `innerHTML` 生成 `DOM` 元素，
这样的做法非常普遍。但是你是否遇到过，如果字符串中拼接的 `HTML` 标签中有 `script` 标签，
那么该段脚本是无法执行的，这并不是 bug，而是 w3c 的文档规定的。

比如如下这段代码，`innerHTML` 插入的脚本`（alert）`并不会执行：

```
<div id="myDiv">
</div>

<script>
  // 模拟接口返回数据
  var strVar = "";
    strVar += "<script>alert('hello world')<\/script>";

  document.getElementById('myDiv').innerHTML = strVar;
</script>
```

那么问题来了，如何使得 innerHTML 进来的 script 代码能够跑起来？