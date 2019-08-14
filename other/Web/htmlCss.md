# HTML和CSS

## 元素都有哪些类型：

* 块状元素
    * display:block
    * &lt;div>、&lt;p>、&lt;h1>...&lt;h6>、&lt;ol>、&lt;ul>、&lt;dl>、&lt;table>、&lt;address>、&lt;blockquote> 、&lt;form> 
    * 标签独占一行，可指定宽、高
* 内联元素(又叫行内元素)
    * display:inline
    * <a>、<span>、<i>、<em>、<strong>、<label>、<q>、<var>、<cite>、<code>
    * 标签在一行内，宽度与高度由内容决定，只有在内容超过HTML的宽度时，才会换行
* 内联块状元素
    * display:inline-block
    * &lt;img>、&lt;input>
    * 同时具备内联元素、块状元素的特点
        * 和其他元素都在一行上
        * 元素的高度、宽度、行高以及顶和底边距都可设置

## 一个块元素垂直水平绝对居中的方法：

flex布局

```css
.box {
    margin: 50vh auto 0;
    transform: translate(0, -50%);
}
```

## css选择器有哪些，选择器的权重的优先级

### 选择器类型

|名称|示例|
|:--:|:--:|
| ID | #id |
| class | .class |
| 标签 | p |
| 通用 | * |
| 属性 | `[type="text"]` |
| 伪类 | :hover |
| 伪元素 | ::first-line |
| 子选择器、相邻选择器 | |

### 权重计算规则

1. 第一等：代表内联样式，如: style=””，权值为1000。
2. 第二等：代表ID选择器，如：#content，权值为0100。
3. 第三等：代表类，伪类和属性选择器，如.content，权值为0010。
4. 第四等：代表类型选择器和伪元素选择器，如div p，权值为0001。
5. 通配符、子选择器、相邻选择器等的。如*、>、+,权值为0000。
6. 继承的样式没有权值。

## 相对定位和绝对定位的差别：

## 隐藏一个元素的方法：

## H5的新特性有哪些：
