# VUX的安装于与使用 试题
#### [作者] 高天阳
#### [邮箱] 13683265113@163.com
#### [版本] v1.0.0
#### [标签] 
* VUX的安装于与使用

## [实战题] 请按照以下步骤完成VUX项目的初始化及使用
#### 标签
* VUX

1. 初始化VUX项目
2. 配置路由
* 要求:
```
按照以下层级结构创建3个页面
VUX
├── home.vue                    # 首页
└── info.vue                    # 资讯页
    └── infoDetail              # 资讯详情页
```
3. 使用VUX组件，编写demo页
* 要求:
```
home页面至少需使用到 XHeader、Group、Cell
info页面至少需使用到 XHeader、Group、XInput
infoDetail页面至少需使用到 XHeader、Group、Cell
```
4. 页面间跳转并传参
* 要求:
```
home页面传参至info页面，使用query传参方式
info页面XInput输入内容传参至infoDetail页面，使用params传参方式
infoDetail页面返回后，info页面输入框重新渲染之前的数据(返回需使用XHeader组件)
```
5. 图片引入
* 要求:
```
编辑info页面，使用三种方式引入图片资源(css、js、img)
```
6. 声明并使用全局变量
* 要求:
```
声明全局变量colorList并在info页面、infoDetail页面调用
const colorList = [
  '#F9F900',
  '#6FB7B7',
  '#9999CC',
  '#B766AD',
  '#B87070',
  '#FF8F59',
  '#FFAF60',
  '#FFDC35',
  '#FFFF37',
  '#B7FF4A',
  '#28FF28',
  '#1AFD9C',
  '#00FFFF',
  '#2894FF',
  '#6A6AFF',
  '#BE77FF',
  '#FF77FF',
  '#FF79BC',
  '#FF2D2D',
  '#ADADAD'
]
const colorListLength = 20
```
7. 声明并使用全局函数
* 要求:
```
声明全局函数并在info页面、infoDetail页面调用
function getRandColor () {
  var tem = Math.round(Math.random() * colorListLength)
  return colorList[tem]
}
```
8. 声明并使用全局样式
* 要求:
```
XHeader组件背景色自定义
Cell组件文字超长隐藏显示省略号
```
9. 引入axios插件并使用
* 要求:
```
在home页面请求服务器数据并展示
```
10. 引入lodash插件并使用
* 要求:
```
在home页面处理服务器数据并展示
```

