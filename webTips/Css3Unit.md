# css所有单位都在这了：px,em,rem,vh,vw……

![](http://p3.pstatp.com/large/28980001eea43cdebe14 "css所有单位都在这了：px,em,rem,vh,vw……")

**小伙伴们，css3单位你们听说过多少？我们在前端切图项目中用到的有px，em，rem，vh，% 其他基本没用到过了。特别是vh ，特别好用。**

**附所有css单位，应该是最全的了**

**px：**绝对单位，页面按精确像素展示

**em：**相对单位，基准点为父节点字体的大小，如果自身定义了font-size按自身来计算（浏览器默认字体是16px），整个页面内1em不是一个固定的值。

**rem：**相对单位，可理解为”root em”, 相对根节点html的字体大小来计算，CSS3新加属性，chrome/firefox/IE9+支持。

**vw：**viewpoint width，视窗宽度，1vw等于视窗宽度的1%。

**vh：**viewpoint height，视窗高度，1vh等于视窗高度的1%。

**vmin：**vw和vh中较小的那个。

**vmax：**vw和vh中较大的那个。

%:百分比

in:寸

cm:厘米

mm:毫米

pt:point，大约1/72寸

pc:pica，大约6pt，1/6寸

ex：取当前作用效果的字体的x的高度，在无法确定x高度的情况下以0.5em计算\(IE11及以下均不支持，firefox/chrome/safari/opera/ios safari/android browser4.4+等均需属性加么有前缀\)

ch:以节点所使用字体中的“0”字符为基准，找不到时为0.5em\(ie10+,chrome31+,safair7.1+,opera26+,ios safari 7.1+,android browser4.4+支持\)

