# markdown培训

#### 作者：高天阳

#### 邮箱：13683265113@163.com

```
更改历史

* 2018-10-10    高天阳    添加表格
* 2018-09-14    高天阳    添加锚点
* 2017-09-08    高天阳    格式化文档
* 2017-07-03    高天阳    初始化文档
```

## 第一章 markdown简介

Markdown 是一个 Web 上使用的文本到HTML的转换工具，可以通过简单、易读易写的文本格式生成结构化的HTML文档。

markdownMarkdown 的目标是实现「易读易写」。

## 第二章 markdown语法

### 2.1 标题

* 类Setext

This is an H1
====
This is an H2
----

```
Code:

This is an H1
====
This is an H2
----
```

```
备注:任何数量的=和-都可以有效果<br/>
=表示最高阶标题,-表示第二阶标题
```

* atx形式

# This is an H1

## This is an H2

### This is an H3

#### This is an H4

##### This is an H5

###### This is an H6

```
Code:

# This is an H1

## This is an H2

### This is an H3

#### This is an H4

##### This is an H5

###### This is an H6
```

```
也可以表示成这样 # This is an H1 #
备注: 行首n个#表示n阶标题，n最大为6
```

### 2.2 列表

* 有序列表

有序列表使用数字接着一个英文句点

1. Bird
2. McHale

```
Code:
1. Bird
2. McHale
```

无序列表

无序列表是使用,+,-中任意一种来表示

- Red
+ Green
* Blue

```
Code:
- Red
+ Green
* Blue
```

### 2.3 引用

区块引用是使用类似email中用>来表示

示例

```
> 简单引用1
> 简单引用2
>
> 多行引用
>> 嵌套引用

> ## 引用中使用Markdown语法。
>
> 1. 这是第一行列表项。
> 2. 这是第二行列表项。
>
> 给出一些例子代码：
>
> return shell_exec("echo $input | $markdown_script");
```

效果

> 简单引用1
> 简单引用2
>
> 多行引用
>> 嵌套引用

> ## 引用中使用Markdown语法。
>
> 1. 这是第一行列表项。
> 2. 这是第二行列表项。
>
> 给出一些例子代码：
>
> return shell_exec("echo $input | $markdown_script");

### 2.4 代码区块

建立代码区块,只需要简单地缩进4个空格或是1个制表符就可以

代码块一直持续到没有缩进的那一行(或是文件的结尾)

代码块
也可以使用` 来表示

使用缩进表示代码块

### 2.5 分隔线

一行中用三个以上的星号、减号、底线来建立一个分隔线,行内不能有其他东西,
也可以在星号或是减号中间插入空格


```

---
```

---

```
- - -
```

- - -

```
***
```

***

```
* * *
```

* * *
```

——————————————
```
——————————————

### 2.6 段落和换行

* 段落

段落是由一个或多个连续的文本行组成,

它的前后要一个以上的空行(显示上看起来像是空的)

* 换行

Mardown允许段落内的强迫换行(插入换行符)<br/>
要依赖Markdown来插入`<br/>`标签的话,在`<br/>`插入处要先按入两个以上的空格然后回车

### 2.7 链接

支持两种形式的连接语法: 行内式和参考式 链接字符不区分大小写
* 行内式
This is [baidu](http://www.baidu.com/ "度娘")
[baidu](https://www.baidu.com/)

```
Code:
This is [baidu](http://www.baidu.com/ "度娘")

[baidu](https://www.baidu.com/)
```

* 参考式
This is [baidu example][id] reference-style link.
[id]: https://www.baidu.com/ "度娘"

```
Code:
This is [baidu example][id] reference-style link.
标记: [id]: https://www.baidu.com/ "度娘"
或者: [id]: https://www.baidu.com/ '度娘'
或者 [id]: https://www.baidu.com/ (度娘)
```

* 隐式链接标记功能
[Baidu][]
标记可以这样写: [Baidu]: http://baidu.com

```
Code:
[Baidu][]
标记可以这样写: [Baidu]: http://baidu.com
```

* 参考式链接范例:
---

```
--I get 10 times more traffic from [Google] [1] than from
--[Yahoo] [2] or [MSN] [3].
--[1]: http://google.com/ "Google"
--[2]: http://search.yahoo.com/ "Yahoo Search"
--[3]: http://search.msn.com/ "MSN Search"
--I get 10 times more traffic from [Google][] than from
--[Yahoo][] or [MSN][].
--[google]: http://google.com/ "Google"
--[yahoo]: http://search.yahoo.com/ "Yahoo Search"
--[msn]: http://search.msn.com/ "MSN Search"
(备注: 上述代码在使用时需删掉前面的--)
```

* 自动链接
https://www.baidu.com

```
示例如下:

http://www.baidu.com
```

### 2.8 强调

Markdown使用性星号(*)和底线(_)作为标记强调字词的符号 两端被一个*或_包围的单词会被转换成斜体 两端被两个*或_包围的单词会被转换成粗体 *或_的两端不能有空白 用什么符号就以什么符号结尾

```
示例
*斜体*
_斜体_
**粗体**
__粗体__
```

### 2.9 代码

如果要标记一段行内代码,可以用反引号 ` 把它包起来 用多个反引号来开启和结束代码区段


``段落代码``
``包含`反引号``
``包含 `两个反引号` ``
``<特殊符号&>``

```
示例:

``段落代码``
``包含`反引号``
``包含 `两个反引号` ``
``<特殊符号&>``
```

### 2.10 图片 Markdown使用一种和链接很相似的语法来标记图片 允许两种样式:行内式和参考式

* 行内式的图片语法:

示例
![September](http://a3.topitme.com/4/9b/8f/11644743891028f9b4o.jpg)
![花瓣网](http://img.hb.aicdn.com/8b794b37c8aa6ec016d87f2608d5bddb2af37d66e7f7-Dhl91t_fw658 "孤影摇动")

```
示例
![September](http://a3.topitme.com/4/9b/8f/11644743891028f9b4o.jpg)
![花瓣网](http://img.hb.aicdn.com/8b794b37c8aa6ec016d87f2608d5bddb2af37d66e7f7-Dhl91t_fw658 "孤影摇动")
```

* 参考式语法:

![花瓣网][xd]
[xd]:http://img.hb.aicdn.com/8b794b37c8aa6ec016d87f2608d5bddb2af37d66e7f7-Dhl91t_fw658 "孤影摇动"


```
示例:
--![花瓣网][xd]
--[xd]:http://img.hb.aicdn.com/8b794b37c8aa6ec016d87f2608d5bddb2af37d66e7f7-Dhl91t_fw658 "孤影摇动"
(备注: 上述代码在使用时需删掉前面的--)
```

### 2.11 锚点

网页中，锚点其实就是页内超链接，也就是链接本文档内部的某些元素，实现当前页面中的跳转。
比如我这里写下一个锚点，点击回到目录，就能跳转到目录。 在目录中点击这一节，就能跳过来。还有下一节的注脚。这些根本上都是用锚点来实现的。

注意： Markdown Extra 只支持在标题后插入锚点，其它地方无效。

语法描述：
在你准备跳转到的指定标题后插入锚点{#标记}，然后在文档的其它地方写上连接到锚点的链接。

代码：

```
## 0. 目录{#index}
跳转到[目录](#index)
```

显示效果：

跳转到目录

### 2.12 转义

使用反斜杠来插入一些在语法中有其它意义的符号,如* 需要转义的字符:

```
\ 反斜线
` 反引号
* 星号
_ 底线
{} 花括号
[] 方括号
() 括弧
# 井字号
+ 加号
- 减号
. 英文句点
! 惊叹号
```

### 2.13 表格

示例：

| 一个普通标题 | 一个普通标题 | 一个普通标题 |
| ------ | ------ | ------ |
| 短文本 | 中等文本 | 稍微长一点的文本 |
| 稍微长一点的文本 | 短文本 | 中等文本 |

代码：

```
| 一个普通标题 | 一个普通标题 | 一个普通标题 |
| ------ | ------ | ------ |
| 短文本 | 中等文本 | 稍微长一点的文本 |
| 稍微长一点的文本 | 短文本 | 中等文本 |
```
