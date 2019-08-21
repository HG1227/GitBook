## HTML5 Plus应用概述

HTML5 Plus移动App，简称5+App，是一种基于HTML、JS、CSS编写的运行于手机端的App，这种App可以通过扩展的JS API任意调用手机的原生能力，实现与原生App同样强大的功能和性能。

## HTML5 Plus规范

通过HTML5开发移动App时，会发现HTML5很多能力不具备。为弥补HTML5能力的不足，在W3C中国的指导下成立了HTML5中国产业联盟www.html5plus.org组织，推出HTML5+规范。目前该联盟已经挂靠在工信部信通院标准所下，相关标准已经成为行业标准。
HTML5+规范是一个开放规范，隶属于工信部，允许三方浏览器厂商或其他手机runtime制造商实现。
HTML5+扩展了JavaScript对象plus，使得js可以调用各种浏览器无法实现或实现不佳的系统能力，设备能力如摄像头、陀螺仪、文件系统等，业务能力如上传下载、二维码、地图、支付、语音输入、消息推送等。
除了功能外，HTML5+很重要的特点是提供了原生的渲染能力，通过plus.webview、plus.nativeObj、plus.nativeUI，让开发者可以使用js来调用原生渲染能力，实现体验的大幅提升。
原生的api多达40万，HTML5+的封装并非把40万api都封装了一遍，而是分成了2个层面：

- HTML5Plus规范：常用的扩展能力，比如二维码、语音输入，都封装到了规范中，同时实现了Android和iOS的解析引擎，使得开发者的代码编写一次，可跨平台运行。
- Native.js是另一项创新技术。手机OS的原生API有四十多万，大量的API无法被HTML5使用。Native.js把几十万原生API映射成了js对象，通过js可以直接调ios和android的原生API。这部分就不再跨平台，写法分别是plus.ios和plus.android，比如调ios game center，或在android手机桌面创建快捷方式，这些都是平台专有的api。

Native.js的用法示例，var obj= plus.android.import("android.content.Intent");，将一个原生对象android.content.Intent映射为js对象obj，然后在js里操作obj对象的方法属性就可以了。
Native.js的详细教程可以参考：5+ App开发Native.js入门指南
在5+App里，同时包含了HTML5Plus规范和Native.js的实现，开发者可以在5+App里自由使用相关技术。

## 5+ App概念解析
首先开发者需要清楚你要做什么，是一个mobile web项目，运行在浏览器里？还是要做一个app，安装和运行在手机上？或者要把一个mobile web项目打包成app？
1. 做一个mobile web项目
在这个模式下，开发者用不到HTML5Plus，使用标准的HTML5语法，运行在浏览器里。这不算5+ App。
此时开发者仍然可以使用HBuilder这个开发工具，新建项目时选择web项目。
开发者也仍然可以使用DCloud提供的mui开源框架，来简化ui的开发。
但这就是一个普通的web项目，b/s方式，不可脱线运行，不能调用HTML5Plus的增加api。
2. 做一个正统的app
传统意义上的app，是c/s方式的，它的程序要安装和运行在手机上，不通过浏览器在线下载。
此时开发者在HBuilder里新建项目时，选择“移动App”。
在移动App项目下编写的HTML、js等文件，是会被打包到原生的安装包（Android是apk包、iOS是ipa包）里的。
此时本地的js和服务器通过ajax交互，由服务器按接口方式给出数据（一般是json），然后客户端的js文件解析json，并根据本地的业务逻辑来渲染页面和执行功能。
所以请不要新建一个移动App项目，然后把本来运行在服务器端的php等文件也都丢到这个项目下。
web项目始终是web项目，哪怕要在app项目里某个界面里，在线加载一个远程的网页，也要把这个远程网页的代码，放到web项目下。
移动App项目下，只有能有html、js、css、json以及一些图片或数据文件，不能包括php、jsp、py等服务器页面。
3. 使用wap2app打包mobile web项目为app
如果开发者想把一个做好的mobile web站，方便快速的打包成app，那么要使用DCloud的wap2app框架。
在HBuilder中新建项目时，选wap2app项目，把mobile web站的url输入进去，参考框架的教程来配置。
wap2app不同于普通的web打包技术，wap2app可真正做达到原生应用的功能和性能体验。
具体教程另见：文档中心-wap2app，http://ask.dcloud.net.cn/docs/#//ask.dcloud.net.cn/article/1244
wap2app属于5+app，它底层也是强大的HTML5Plus规范和Native.js在支撑。
wap2app项目下的所有文件，也都是打包在本机运行的。
4. 如果你想开发一次，全端覆盖，那么需要使用mui框架
具体参考：http://ask.dcloud.net.cn/docs/#//ask.dcloud.net.cn/article/591

## HTML5+ 应用架构
![blockchain](http://www.dcloud.io/docs/a/h5p/architecture.png "应用架构")

## HTML5+ 规范 API 及demo示例
最新规范请参考http://www.html5plus.org/#specification
手机端体验各个API的实现效果，ios手机在Appstore搜索Hello H5+，Android手机下载地址。
在HBuilder中新建移动App，选Hello H5+，即可看到这个demo的源代码。

## 开发环境HBuilder
HBuilder内置HTML5+ APP开发环境，提供一套完整的移动应用开发解决方案。内置HTML5+ API语法提示，提高开发效率；集成真机运行环境，方便开发后即时在真机上查看运行效果；集成应用云端打包系统，不用部署xcode和Android sdk就可以打包应用。使开发者只需要使用HTML5、Javascript、CSS技术就可以快速开发跨平台的移动应用。
下载地址：http://www.dcloud.io/

平台支持
iOS 5.0及以上
Android 2.3及以上


### 问题 IOS 和 Android的安装包扩展名分别是什么
.apk

### App项目能否包含以下文件php、jsp？

* [uniapp官方文档](http://uniapp.dcloud.io/)
