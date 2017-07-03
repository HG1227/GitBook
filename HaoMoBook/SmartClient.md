# SmartClient {#smartclient}

## 第一章 SmartClient介绍 {#第一章-smartclient介绍}

### 1.1 SmartClient介绍 {#11-smartclient介绍}

Smart Client简称智能客户端，是Microsoft推出的一种将B/S（瘦客户端）和C/S（胖客户端）结合在一起的一种技术。

就是这样一种一个可扩展的能集成不同应用的桌面应用程序：它可以无接触部署、即需即装、动态加载，XCopy即可运行而无须修改注册表，可以动态升级、自动更新，可以方便的经Web运行而不用担心防火墙问题并可以方便的离线运用，方便的连接WebServices的Windows应用程序。

### 1.2 SmartClient特点 {#12-smartclient特点}

1.易于升级\(自动更新\)  
类似于B/S架构的程序，只要在服务器上更新软件，进行简单配置，客户端会自动进行软件的更新。比如在服务器的站点上建立一 个虚拟目录，将客户端应用程序发布到该虚拟目录中，客户通过HTTP方式安装更新程序。  
2.富客户端，强大的用户界面，更好的用户体验  
Smart Client可以使用WinForm开发Client端程序，可以充分使用Winform上的各种控件和资源，突破B/S（瘦客户端）在表现能力上的限制，WEB如果实现某些功能可能必须通过ActiveX或Applet。  
3.充分利用Client端资源  
充分使用客户端的软件资源和硬件资源。  
4.可以支持在线使用和离线使用  
B/S程序需要实时的网络连接，数据交换和数据处理需要反复的请求响应，需要反复刷新页面。Smart Client允许用户将数据下载到Client端进行离线的数据处理，当用户重新连接网络时，可以手动或者自动向服务端提交更新数据。  
5.个性化用户界面  
用户可根据喜好自行设置客户端应用程序，配置信息将被保存到服务器上。

## 第二章 SmartClient的安装使用 {#第二章-smartclient的安装使用}

### 2.1 SmartCLient的安装及使用 {#21-smartclient的安装及使用}

第一步：[http://www.smartclient.com/;quSmartClient官网下载LGPL版本，并解压缩；](http://www.smartclient.com/;quSmartClient%E5%AE%98%E7%BD%91%E4%B8%8B%E8%BD%BDLGPL%E7%89%88%E6%9C%AC%EF%BC%8C%E5%B9%B6%E8%A7%A3%E5%8E%8B%E7%BC%A9%EF%BC%9B)  
第二部：运行解压后目录下的\SmartClient\_60\_LGPL\smartclientSDK\start\_embedded\_server.bat，SDK自带了一个内嵌的tomcat

## 第三章 SmartClient常用组件介绍 {#第三章-smartclient常用组件介绍}

3.1 DynamicForm（表单布局组件）

DynamicForm 继承至Canvas组件。  
DynamicForm管理一组用于用户输入组件FormItem的集合。DynamicForm提供各个FormItem之间的布局、值的管理，同时也提供各个FormItem的验证和数据绑定的管理。

效果图:

![](https://hxgqh.gitbooks.io/haomotraining/content/assets/WechatIMG83.jpeg)

示例:

```
isc.DynamicForm.create({
    width: 250,
    fields: [
        {name: "username",title: "Username",type: "text",required: true,defaultValue: "bob"},
        {name: "email",title: "Email",required: true,type: "text",defaultValue: "bob@isomorphic.com"},
        {name: "password",title: "Password",required: true,type: "password",
         validators: [{
            type: "matchesField",
            otherField: "password2",
            errorMessage: "Passwords do not match"
         }]
        },
        {name: "password2",required: true,wrapTitle: false,title: "Password again",type: "password"},
        {name: "createAccount",title: "Create Account",type: "button",click: "form.validate()"}
    ]
});

```

3.2 ListGrid（列表布局组件）

效果图:

![](https://hxgqh.gitbooks.io/haomotraining/content/assets/WechatIMG82.jpeg)

示例:

```
isc.ListGrid.create({
    ID: "countryList",
    width:500, height:224, alternateRecordStyles:true, 
    fields:[
        {name:"countryCode", title:"Code"},
        {name:"countryName", title:"Country"},
        {name:"independence", title:"Nationhood", type:"date", width:100},
        {name:"population", title:"Population", type:"integer"},
        {name:"gdp", title:"GDP", type:"float"}
    ],

})

```

3.3 Ibutton（按钮）

效果图:

![](https://hxgqh.gitbooks.io/haomotraining/content/assets/WechatIMG85.jpeg)

示例:

```
isc.IButton.create({
    title: "Hello",
    icon: "icons/16/world.png",
    iconOrientation: "right",
    click: "isc.say('Hello world!')"
})

```

3.4 TabSet（标签布局组件）

TabSet组件让多个Tab组件可共享一块区域，其中一个Tab页被用户选中后，显示在TabSet组件的区域中。TabSet继承至Canvas。

效果图:

![](https://hxgqh.gitbooks.io/haomotraining/content/assets/WechatIMG84.jpeg)

示例:

```
isc.TabSet.create({
    ID: "tabSet",
    tabBarPosition: "top",
    width: 430,
    height: 200,
    canEditTabTitles: true, 
    titleEditEvent: "doubleClick",
    titleEditorTopOffset: 2,
    tabs: [
        {title: "Blue", canClose: true,
         pane: isc.Img.create({autoDraw: false, width: 48, height: 48, src: "pieces/48/pawn_blue.png"})},
        {title: "Green", canClose: true,
         pane: isc.Img.create({autoDraw: false, width: 48, height: 48, src: "pieces/48/pawn_green.png"})},
    ]
});

```

3.5 Menu（菜单）

菜单类\(Menu\)实现互动式菜单控件,并可选配图标,子菜单和快捷键,通常用于表格和树的右键菜单，和工具栏的下拉菜单。

效果图:

![](https://hxgqh.gitbooks.io/haomotraining/content/assets/WechatIMG86.jpeg)

示例:

```
isc.Menu.create({
    ID:"customColumnMenu",
    autoDismiss:false,
    fields:[
        "title", 
        {name:"canDismiss", width:16,showValueIconOnly:true,
         valueIcons:{
            "true":"icons/16/close.png"
         }
        }
    ],
    data:[
        {name:"Item 1"},
        {name:"Item 2", canDismiss:true},
        {name:"Item 3", canDismiss:true}
    ]
});

isc.HStack.create({
    width: "100%",
    members: [customColumnMenu]
});

```

3.6 VLayout／HLayout（布局组建）

SmartClient主要常用水平布局（HLayout）、垂直布局（VLayout）等布局方式。

效果图:

![](https://hxgqh.gitbooks.io/haomotraining/content/assets/WechatIMG87.jpeg)

示例:

```
isc.HLayout.create({
    width: "100%",
    height: "100%",
    members: [
        isc.Label.create({
            contents: "Navigation",
            align: "center",
            overflow: "hidden",
            width: "30%",
            showResizeBar: true,
            border: "1px solid blue"
        }),
        isc.VLayout.create({
            width: "70%",
            members: [
                isc.Label.create({
                    contents: "Listing",
                    align: "center",
                    overflow: "hidden",
                    height: "30%",
                    showResizeBar: true,
                    border: "1px solid blue"
                }),
                isc.Label.create({
                    contents: "Details",
                    align: "center",
                    overflow: "hidden",
                    height: "70%",
                    border: "1px solid blue"
                })
            ]
        })
    ]
});

```

## 第四章 SmartClient的发展 {#第四章-smartclient的发展}

Smart Client实际上是一个客户端表现层架构，通过抽象这些概念开发人员可以更好地理解现代软件开发的各个层次。它最适合的是.NET平台，而.NET则是微软的战略基础，相信微软在几年内，会有越来越多的应用构建在.NET之上。在未来的几年之内，.NET将成为更加主流的应用平台，作为建立在.NET基础之上的抽象的表现层架构，随着.NET平台的更加成熟，Smart Client也会有更多的用武之地。

