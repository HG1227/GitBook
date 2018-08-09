# innerHTML引入的script如何使用

#### 作者：高天阳
#### 邮箱：13683265113@163.com

```
更改历史

* 2018-8-9      高天阳	    初始化文档

```



### 2.3 ~~document.write~~

document.write 接收一个字符串作为参数，并且支持 script 标签以及其他 HTML 标签拼成的字符串，看起来似乎是完美的方案。
不过鉴于 document.write 的怪属性，只适合 strVal 在首页输出流中的渲染情况，如果是异步的请求，就可以放弃了。

code：

```
hello world
<script src="http://apps.bdimg.com/libs/jquery/2.1.4/jquery.min.js"></script>
<div>
<script>
    $.get('data.php', function(data) {
      document.write(data);
    })
</script>
</div>
```

目的似乎是为了在 div 中嵌入 data，但是 hello world 字样也消失了，很显然，异步请求后重启输入流，将页面全部覆盖掉了。

### 2.4 jQuery html() 方法

使用封装过的方法无疑是个好办法：

```
<div id="myDiv"></div>
<script src="http://apps.bdimg.com/libs/jquery/2.1.4/jquery.min.js"></script>
<script>
  $.get('data.php', function(data) {
    $('#myDiv').html(data);
  })
</script>
```

如果已经引入了 jQuery，无疑是最佳方案，没必要重复造轮子了。

### 2.5 利用 img 标签

黑魔法，如果后台接口可控的话。

比方说我希望 innerHTML 的内容如下：

```
<div></div>
<script>
  alert('hello world');
</script>
```

我们可以这样构造 img：

```
<div id='myDiv'></div>
<script>
  var str = "<div></div>";
  str += "<img src='empty.gif' onload='alert(\"hello world\"); this.parentNode.removeChild(this);' />";
  document.getElementById('myDiv').innerHTML = str;
</script>
```

### 2.6 特殊的 IE

事实上，一定条件下，innerHTML 进来的 script 脚本，在 IE（IE9-？）下是可以触发的。

需要满足的条件如下：

* 脚本有 defer 属性
* 脚本并不是 innerHTML 的第一个元素（ script 元素必须位于 "有作用域的元素" 之后。
如果通过innerHTML 插入的字符串开头就是一个 "无作用域的元素"，那么 IE 会在解析这个字符串前先删除该元素）

code：

```
<body> 
<div id='myDiv'></div>
<script type="text/javascript">
  var strVar = "";
  strVar += "<span style='display: none'>hack ie</span><script defer='true'>";
  strVar += "alert('hello world');";
  strVar += "<\/script>";

  document.getElementById("myDiv").innerHTML = strVar;
</script>
</body>
```

## 参考资料

* [让innerHTML进来的script代码跑起来](http://www.cnblogs.com/zichi/p/run-innerHTML-script.html)