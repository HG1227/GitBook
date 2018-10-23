# Ajax的深度解析

#####作者：王志伟
#####邮箱：wangzhiwei@yumaomoney.com

```
更改历史

*2018-10-23     高天阳     迁移jquery使用Ajax示例
*2018-10-17     王志伟     初始化文档

```

##1 什么是Ajax

Ajax全称：Asynchronous JavaScript and XML
Ajax不是某种变成语言
而是一种无需重新加载整个网页的情况下能够更新部分网页的技术。

###1.1 同步
![](../../assets/ajax/ajax-1.jpg)

###1.2 异步
![](../../assets/ajax/ajax-1.jpg)

##2 XMLhHttpRequest对象
###2.1 创建XMLhHttpRequest对象
```
    //实例化XMLhHttpRequest对象
    var XHR = new XMLHttpRequest();
```
IE6以下浏览器不支持XMLhHttpRequest对象
```
    if(window.XMLHttpRequest === undefined){
        window.XMLHttpRequest = function(){
            try{
                //如果可用，则使用ActiveX对象最新版本
                return new ActiveXObject("Msxml2.XMLHTTP.6.0");
            }
            catch(e1){
                try{
                    //否则，回退到较旧的版本
                    return new ActiveXObject("Msxml2.XMLHTTP.3.0");
                }
                catch(e2){
                    //否则，抛出错误
                    throw new Error("XMLHttpRequest is not supported");
                }
            }
        }
    }
```


##2.2 XMLhHttpRequest和本地文件
开发和测试时XMLhHttpRequest对象的使用差异
![](../../assets/ajax/ajax-3.jpg)

##2.3 了解HTTP
*Http 是计算机通过网络进行通信的规则
*http 是一种无状态的信息
是指比如客户获得一张网页之后关闭浏览器，然后再一次启动浏览器，再登录该网站，但是服务器并不知道客户关闭了一次浏览器

一个完整的HTTP请求，通常包括7个步骤
* 建立TCP链接
* Web浏览器向Web服务器发送请求命令
* Web浏览器发送请求头部信息
* Web服务器应答
* Web服务器发送应答头信息
* Web服务器向Web浏览器发送数据
* Web服务器关闭TCP连接

##一个HTTP请求包括四个部分
* HTTP请求方法或“动作”GET/POST
* 正在请求的地址(url)
* 一个可选的请求头集合，其中可能包括身份验证信息(客户端环境信息)
* 一个可选的请求主体（查询字符串、表单信息）

##服务器返回HTTP响应包括3个部分
* 一个数字和文字组成的状态码，用来显示请求的成功和失败
* 一个响应头集合
* 响应主体

![](../../assets/ajax/ajax-4.jpg)

##2.4 GET请求与POST请求的差异
##GET
* 一般用于信息获取
* 使用URL传递参数
* 对发送的信息数量有限制 2000个字符

##POST
* 一般用于修改服务器上的资源
* 对所发的信息数量无限制

##2.5 HTTP状态码
![](../../assets/ajax/ajax-5.jpg)

##2.6 XMLHttpRequest发送请求
`open(method,url,async)`
`send(string)`

```
request.open("GET","get.php",true);
request.send()
```
```
request.open("POST","get.php",true);
request.send()
```
```
request.open("GET","create.php",true);
request.setRequestHeader("Content-type","application/x-www-form-urlencoded");
request.send("name=高天阳&age=26");
```

##2.7 XMLHttpRequest取得响应
![](../../assets/ajax/ajax-6.jpg)
![readyState属性](../../assets/ajax/ajax-7.jpg)

```
    var request = new XMLHttpRequest();
    request.open("GET","get.php",true);
    request.send();
    request.onreadystatechange = function(){
        if(request.readyState ===4&& request.status===200){
            request.responseText
            //做你的操作
        }
    }
```
应用场景？



###3.JSON基本概念
JSON:Javascript对象表示法（Javascript Object Notation）
JSON是存储和交换文本信息的语法，类似XML。它采用键值对的方式来组织，易于人们阅读与编写，同时也易于机器解析与生成。
JSON是独立语言，也就是说不管什么语言都可以解析Json,只需要按照JSON的规则即可
```
var jsonStr='{"result":[{"name":"zhiwei","age":"18"},{"name":"gaogao","age":"20"},{"name":"xiaoyu":"age":"14"}]}'
```
##3.1 解析JSON
eval和JSON.parse()的区别

禁止使用eval的原因


```
var jsonStr='{"result":[{"name":"zhiwei","age":"18"},{"name":"gaogao","age":"20"},{"name":"xiaoyu","age":"14"}]}'

//var jsonObject =eval('('+jsonStr+')');
//var jsonObject = JSON.parse(jsonStr);
alert(jsonObject[0].age)
```
如果在解析对象的同事 格式化对象属性 将age的数据转化成出生年份
推荐json检测工具
https://jsonlint.com/

##规范的JSON返回值
```
{
    "status":"success"
    "msg":"not find"
    "data":{
        "name":"zhiwei..."
    }
}
```

##4.Jquery中的ajax使用

```
$.ajax({
    type: 'GET', 
    url: '999.php', 
    data: {
        uname:'Tom', age: 20
    }, 
    beforeSend: function(){ 
        console.log('before send....'); 
        console.log(arguments); 
    }, 
    success: function(){ 
        console.log('success....'); 
        console.log(arguments); 
    }, 
    error: function(){ 
        console.log('error....'); 
        console.log(arguments); 
    }, 
    complete: function(){ 
        console.log('complete....'); 
        console.log(arguments); 
    } 
});
```

##5.跨越问题
![](../../assets/ajax/ajax-8.jpg)

Javascript出于安全方面的考虑，不允许跨域调用其他页面的对象、什么是跨域呢，简单地理解就是因为Javascript同源策略的限制
##5.1判断跨域
![](../../assets/ajax/ajax-9.jpg)
##5.2如何解决跨域
方法一 代理
![](../../assets/ajax/ajax-10.jpg)

方法二 JSONP
解决主流浏览器Get请求 不支持POST请求
![](../../assets/ajax/ajax-11.jpg)
```
$.ajax({
    type:"GET",
    url:"url",
    dataType:"jsonp",
    jsonp:"callback",
    success:function(){
    ...
    }
})
```
服务器端的改动

![](../../assets/ajax/ajax-12.jpg)

方法二 XHR2
![](../../assets/ajax/ajax-13.jpg)

相关面试题
##1、ajax的实现和原理
##2、Ajax的优缺点各说三条
##3、AJAX机制，open的参数是什么
##4、请解释 JSONP 的工作原理，以及它为什么不是真正的 AJAX
##5、XMLHttpRequest对象在IE和Firefox中创建方式有没有不同
  //IE中通过new ActiveXObject()得到，Firefox中通过newXMLHttpRequest()得到
##6、常见状态码的含义
* 200 OK 客户端请求成功
* 301 资源(网页等)被永久转移到其他URL
* 400 Bad Request 客户端请求有语法错误，不能被服务器所理解
* 403 Forbidden 服务器收到请求，但是拒绝提供服务
* 404 Not Found 请求资源部存在，输入了错误的URL
* 500 Internal Server Error 服务器发生不可预期的错误
* 503 Server Unavailable 服务器当前不能处理客户端的请求，一段时间后可能恢复正常。