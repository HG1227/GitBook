## 20160314更新

后面的项目发现，还有两个坑，需要注意下：

·本文的解决方案的核心是利用了 微信/易信 在ready的时候会有个 WeixinJSBridgeReady/YixinJSBridgeReady事件，通过监听这个事件来触发的。那有个坑就是 如果微信已经ready了，但还没执行到你监听这个ready事件的代码，那么你的监听是没用的，所以\*\*监听的js一定要放在head前面\(放在css外链之前\)，确保最新执行，\*\*切记！切记！

·另一个坑就是，本文的解决方案只适合一开始就播放的背景音乐。如果你是做那种微信场景（打开页面模拟收到很多条微信，每条微信都要播放那段音效），实际上本文的解决方案是不行的。因为ready的事件只会执行一次，即使你在ready事件里面用setTimeout或者setInterval也可能会导致丢失情况。

### ---------------------------------------------------------------------------------------

## 前言

在做各种HTML5场景页面的时候，插入背景音乐是一个很普遍的需求。我们都知道，IOS下的safari是无法自动播放音乐的，以至一直以来造成一种错误的认识，iso是无法自动播放媒体资源的。直到微信火爆起来，我们发现IOS的微信里面打开的页面却可以实现自动播放。这种情况颠覆了我之前的认知。但是，但是。。。最近的项目，又发现了一个头疼的问题。部分的IOS微信，打开有自动播放背景音乐的页面没有声音！！最头疼的是同款机子，相同的IOS系统，相同的微信版本！！没错，前端就是要经常这么折腾的，同一个问题，你以为找到了最终的解决方案，但是各种浏览器更新快速，昨天没问题，也许今天就有问题了。还好，这个问题暂时找到原因了，详情请看下文。

## 解决方案

先看下平时使用audio标签插入背景音乐的代码：

`<audio id="Jaudio" class="media-audio" src="bg.mp3" autoplay preload loop="loop"></audio >`

正常来说，上面的写法在安卓和大部分IOS机子的微信是可以播放的（safari这里就忽略讨论），可以扫一扫demo测试下你的手机或者[点击查看demo&gt;&gt;](http://www.w3cmark.com/demo/html5-audio/index2.html)：

如果上面的demo，你的ios微信可以播放，说明你的是大部分正常的手机。如果不能播放，哈哈，你成为了少部分不能正常播放的幸运者。。。

那代码有办法解决这少部分用户呢？如何解决呢？

答案的关键就是微信的WeixinJSBridgeReady事件。这个是微信自带提供的事件，测试发现，上面说的少部分的机子微信只要做微信ready后执行播放，就可以用代码实现自动播放功能了！具体代码请看下面：

`<audio id="Jaudio" class="media-audio" src="bg.mp3" preload loop="loop"></audio >`

`function audioAutoPlay(id){`  
`var audio = document.getElementById(id);`  
`audio.play();`  
`document.addEventListener("WeixinJSBridgeReady", function () {`  
`audio.play();`  
`}, false);`  
`}`  
`audioAutoPlay('Jaudio');`  
刚才如果你第一个demo不能播放的童鞋可以再扫一扫测试下或者[点击查看demo&gt;&gt;](http://www.w3cmark.com/demo/html5-audio/index.html)（如果第一个demo已经测试正常的，这个肯定是正常的啦）

是不是听到声音了呢？！！解决方案就是这么简单。

## 后语

总结下吧，关于音乐自动播放的问题，现在可以分为三种：

1-支持audio的autoplay，大部分安卓机子的自带浏览器和微信，大部分的IOS微信（无需特殊解决）

2-不支持audio的autoplay，部分的IOS微信（本文提供的解决方案）

3-不支持audio的autoplay，部分的安卓机子的自带浏览器（比如小米，开始模仿safari）和全部的ios safari（这种只能做用户触屏时就触发播放了）

那么针对已知的三种情况，关于自动播放背景音乐的问题，我们来总结一下综合解决方案代码吧：

`<!DOCTYPE HTML>`  
`<html>`  
`<head>`  
`<meta charset="utf-8">`  
`<meta name="format-detection" content="telephone=no"/>`  
`<title>IOS微信</title>`  
`<meta name="keywords" content=""/>`  
`<meta name="description" content=""/>`  
`<script type="text/javascript">`  
`//原来是在微信易信执行Ready之前，先注册事件，所以放在所有请求的最前面`  
`document.addEventListener("WeixinJSBridgeReady", function () {`  
`audioAutoPlay('Jaudio');//给个全局函数`  
`}, false);`  
`document.addEventListener('YixinJSBridgeReady', function() {`  
`audioAutoPlay('Jaudio');//给个全局函数`  
`}, false);`  
`</script>`  
`<!-- 加载css放这里 -->`  
`</head>`  
`<body>`

`<audio id="Jaudio" class="media-audio" src="http://game.163.com/weixin/gfxm3_gc/images/bg.mp3" preload loop="loop">`  
`</audio>`

`<script>`  
`function audioAutoPlay(id){//全局控制播放函数`  
`var audio = document.getElementById(id),`  
`play = function(){`  
`audio.play();`  
`document.removeEventListener("touchstart",play, false);`  
`};`  
`audio.play();`  
`document.addEventListener("touchstart",play, false);`  
`}`

`var isAppInside=/micromessenger/i.test(navigator.userAgent.toLowerCase())||/yixin/i.test(navigator.userAgent.toLowerCase());`  
`if(!isAppInside){//给非微信易信浏览器`  
`audioAutoPlay();`  
`}`  
`</script>`  
`</body>`  
`</html>`

## [w3cmark \(http://www.w3cmark.com/2016/434.html\)](http://www.w3cmark.com/2016/434.html)



