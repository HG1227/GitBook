# vux-uploader使用

#### 作者：高天阳
#### 邮箱：13683265113@163.com

```
更改历史

* 2018-10-29        高天阳     初始化文档

```

## 1 简介与特点

### 1.1 简介

vux-uploader是一个vue的上传组件，是对vux组件库的一个补充。

因为vux并没有对weui的uploader组件进行封装，理由见vux issue 682，但这又是一个常见需求。
在使用vux过程中，作者实现了这个组件，现整理开源出来，命名为vux-uploader。

### 1.2 特点

* 基于vux，适合vux项目
* 暂时不支持vux $t方式的多语言功能
* 增加了删除按钮，点击则删除第一张图片
* 内置图片上传、增加、删除功能，但暂时每次只能操作一张图片
* 接上，允许用户监听事件，自己实现上传、增加、删除功能
* 使用axios进行图片上传

## 2 快速使用

### 2.1 检查项目是否符合使用条件

* 需要是使用vux2的项目
* 需要安装babel对ES6部分语法进行转码
* 需要安装less-loader正确编译less源码
* 只支持webpack的方式，暂不提供umd版

### 2.2 安装`vux-uploader`

```
npm install vux-uploader --save

npm install --save-dev babel-preset-es2015
```

### 2.3 配置`.babelrc`

```
{
  "presets": [
    ["env", {
      "modules": false,
      "targets": {
        "browsers": ["> 1%", "last 2 versions", "not ie <= 8"]
      }
    }],
    "es2015",
    "stage-2"
  ],
  "plugins": ["transform-runtime"],
  "env": {
    "test": {
      "presets": ["env", "es2015", "stage-2"],
      "plugins": ["istanbul"]
    }
  }
}
```
### 2.4 使用`vux-uploader`

```
// 引入组件
import Uploader from 'vux-uploader'
```

```
// 子组件
export default {
  ...
  components: {
    ...
    Uploader,
    ...
  }
  ...
}
```

```
// 使用组件
<uploader
    :max="varmax"
    :images="images"
    :handle-click="true"
    :show-header="false"
    :readonly="true"
    :upload-url="uploadUrl"
    name="img"
    :params="params"
    size="small"
    @preview="previewMethod"
    @add-image="addImageMethod"
    @remove-image="removeImageMethod"
></uploader>
```

### 2.5 props说明

* images
    * 类型: Array
    * 默认值: []，空数组
    * 含义: 图片数组，格式为 `[ { url: '/url/of/img.ong' }, ...]`
    * 备注: 变量为数组时，数据流为双向，在组件内部改变数组的值影响父组件
* max
    * 类型: Number
    * 默认值: 1
    * 含义: 图片最大张数
    * 备注: 图片达到max值时，新增按钮消失
* showHeader
    * 类型: Boolean
    * 默认值: true
    * 含义: 是否显示头部
    * 备注: 控制整个头部的显示
* title
    * 类型: String
    * 默认值: 图片上传
    * 含义: 头部的标题
    * 备注: 不显示则留空
* showTip
    * 类型: Boolean
    * 默认值: true
    * 含义: 是否显示头部数字部分，即1/3部分
    * 备注: 当showHeader为false时，header整体隐藏，此时本参数无效
* readonly
    * 类型: Boolean
    * 默认值: false
    * 含义: 是否只读
    * 备注: 只读时，新增和删除按钮隐藏
* handleClick
    * 类型: Boolean
    * 默认值: false
    * 含义: 是否接管新增按钮的点击事件，如果是，点击新增按钮不再自动出现选择图片界面
    * 备注: true时，点击新增按钮，则$emit('add-image')，可以在此事件内进行自定义的选择图片等操作,此后图片的新增、上传、删除都由使用者接管
* autoUpload
    * 类型: Boolean
    * 默认值: true
    * 含义: 选择图片后是否自动上传。是，则调用内部上传接口。否，则$emit('upload-image', formData)',formData`为图片内容，用户可监听事件自己上传
    * 备注: handleClick为true时，无法进行图片选择，故此参数无效。此参数为false时，选择图片后,$emit('upload-image', formData)',formData`为图片内容
* uploadUrl
    * 类型: String
    * 默认值: ''
    * 含义: 接收上传图片的url
    * 备注: 需要返回如下格式的json字符串，否则请设置autoUpload为false自行上传

```
 { 
    result: 0,
    message: "result不是0时候的错误信息",
    data: {
      url: "http://image.url.com/image.png"
    }
  }
```

* name
    * 类型: String
    * 默认值: img
    * 含义: 默认上传的时候，图片使用的表单name
    * 备注: 无
* params
    * 类型: Object
    * 默认值: null
    * 含义: 上传文件时携带参数
    * 备注: 无
* size
    * 类型: String
    * 默认值: normal
    * 含义: 尺寸类型
    * 备注: normal为weui默认尺寸，small为作者定义的小一些的尺寸
* capture
    * 类型: String
    * 默认值: ''
    * 含义: input 的capture属性
    * 备注: 可以设置为camera，此时点击新增按钮，部分机型会直接调起相机，注意，各型号手机表现不同，请谨慎使用。handleClick为true时，此属性无效

### 2.6 emit事件说明

* add-image
    * emit时机: 当handleClick参数为true时，点击新增按钮
    * 参数: 无
    * 备注: 无
* remove-image
    * emit时机: 当handleClick参数为true时，点击删除按钮
    * 参数: 无
    * 备注: 当handleClick为false时，点击删除按钮，组件内部删除第一张图片；否则，用户需要监听本事件，并进行相应删除操作
* preview
    * emit时机: 点击任意一张图片的时候
    * 参数: 图片对象，格式为 { url: 'imgUrl' }
    * 备注: 暂时没有实现自动预览功能，如果需要用户监听事件自行实现
* upload-image
    * emit时机: handleClick和autoUpload都为false`时，选择图片
    * 参数: formData,图片内容生成的formData
    * 备注: 可以通过vm.$refs.input获取图片的input元素

## 参考资料

* [上传图片组件](https://www.npmjs.com/package/vux-uploader)
* [上传图片组件引入报错](https://blog.csdn.net/wandoumm/article/details/80167708)
