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

## 2 解决方案

### 2.1 重新构造 script 标签

思路非常简单，构造新的 script 标签，然后该标签的 innerHTML 赋值为需要渲染的脚本。伪代码如下：

```
var s = document.createElement('script');
s.innerHTML = text;
document.body.appendChild(s);
```

当然如果要写的完美一点，执行完 s 后还需要 `remove` 掉。如何获取 text 值？两个方法，其一可以正则匹配 `strVal`，
提取 `script` 标签内的内容，这点和 BigRender 类似，而 BigRender 除了提取 script 标签，还需要提取 `style` 标签，
无疑更复杂；第二个方法是可以用 `document.getElementsByTagName('script')` 获取插入 DOM 但并未执行的 `script` 脚本，
但是这样会把页面所有脚本全部提取，所以还需要判断。（可以获取某一节点下的 `script` 标签）

如果是外部的 js 文件，需要为新建的 script 元素添加 src 属性即可。

### 2.2 eval 大法

事实上，如果是 `inline` `JavaScript`，方案一求得的 `text`，可以直接 `eval` 之。

但是如果是外联 `js` 文件，同上，需要新建 `script` 标签然后指定 `src` 属性。