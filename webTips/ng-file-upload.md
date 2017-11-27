# ng-file-upload-Angular上传图片插件

#### 作者：高天阳
#### 邮箱：13683265113@163.com

```angular2html
更改历史

* 2017-11-26	高天阳	初始化文档

```

## 1 简介、特点

### 1.1 简介

ng-file-upload是一款轻量级、跨浏览器的angular上传文件指令

### 1.2 特点
        
1. 支持文件上传进度条、取消、暂停
1. 支持文件拖放和黏贴图像
1. 支持暂停和取消文件上传
1. 支持验证文件的类型 / 大小、图像宽度 / 高度、视频 / 音频持续时间（ng-required）
1. 支持预览显示选择的图像、视频、音频
1. 支持CORS和直接上传文件的二进制数据( Upload.$http() )

## 2 安装、使用

### 2.1 安装

* Npm安装

```angular2html
npm install ng-file-upload --save
```

* Bower安装

```angular2html
bower install ng-file-upload --save
```

![](/assets/ng-file-upload1.jpeg)

### 2.2 引入依赖

引入ng-file-upload

```angular2html
//inject directives and services. 
var app = angular.module('fileUpload', ['ngFileUpload']);

app.controller('MyCtrl', ['$scope', 'Upload', function ($scope, Upload) {
    // upload later on form submit or something similar 
    $scope.submit = function() {
      if ($scope.form.file.$valid && $scope.file) {
        $scope.upload($scope.file);
      }
    };
 
    // upload on file select or drop 
    $scope.upload = function (file) {
        Upload.upload({
            url: 'upload/url',
            data: {file: file, 'username': $scope.username}
        }).then(function (resp) {
            console.log('Success ' + resp.config.data.file.name + 'uploaded. Response: ' + resp.data);
        }, function (resp) {
            console.log('Error status: ' + resp.status);
        }, function (evt) {
            var progressPercentage = parseInt(100.0 * evt.loaded / evt.total);
            console.log('progress: ' + progressPercentage + '% ' + evt.config.data.file.name);
        });
    };
    // for multiple files: 
    $scope.uploadFiles = function (files) {
      if (files && files.length) {
        for (var i = 0; i < files.length; i++) {
          Upload.upload({..., data: {file: files[i]}, ...})...;
        }
        // or send them all together for HTML5 browsers: 
        Upload.upload({..., data: {file: files}, ...})...;
      }
    }
}]);
```

![](/assets/ng-file-upload2.jpeg)
![](/assets/ng-file-upload3.jpeg)

### 2.3 使用

在页面插入上传按钮

![](/assets/ng-file-upload5.jpeg)

调用上传接口(把图片对象上传后台)

![](/assets/ng-file-upload4.jpeg)

## 3 涉及参数：

* 文件选择：----适用于：`<button>`、`<div>`、`<input　type=file>`

|参数|注释|
|----|---|
|ngf-select=“true”|默认为true,使得在这个元素上可以选择文件|
|ng-model="myfiles"|将选择的一个或多个文件与scope模型绑定（通过ngf-multiple和ngf-keep的值可以使得ng-model的值为一个数组或单个文件）|
|ng-model-rejected="rejfiles"|与不匹配接受通配符的丢弃文件绑定|
|ng-disabled="selectDisabled"|与一个boolean值绑定，来决定是否禁用文件选择功能|
|ngf-change="fileSelected($files, $file, $event, $rejectedFiles)"|当文件被选择或移除时调用|
|ngf-multiple="true"|默认为false，为true时表示可以选择多个文件|
|ngf-capture="'camera'" or "'other'"|允许移动设备使用相机捕获|
|accept="image/*"|标准的HTML文件接受的输入属性（依赖于浏览器）|
|ngf-accept=" 'image/*' "|用逗号分隔允许的MIME类型来过滤文件|

```angular2html
ngf-validate="{
     size: {min: 10, max: '20MB'},
     width: {min: 100, max:10000}, 
     height: {min: 100, max: 300}, 
     duration: {min: '10s', max: '5m'}, 
     accept: '.jpg'
 }" //  或者 "validate($file)"
```

|参数|注释|
|---|---|
|ngf-keep="true" or "false"|默认为false,保存着以前ng-model的值和追加的新文件|
|ngf-keep-distinct="true" or "false"|默认为false，如果ngf-keep设置了的话，则删除重复的选定文件|
|ngf-reset-on-click="true" or "false"|默认为true，可以重置模型和点击输入|
|ngf-reset-model-on-click="true" or "false"|默认为true，单击时重置模型|

* 文件删除：----适用于：`<button>`、`<div>`

> 注：除了ngf-drop 、ng-model 、 ngf-change之一，其余属性都是可选的

|参数|注释|
|--|--|
|ngf-drop="true" or "false"|默认为true,使得在该元素上可以删除文件|
|ng-model="myFiles"|把被删除的文件与scope模型绑定（通过ngf-multiple和ngf-keep的值可以使得ng-model的值为一个数组或单个文件）|
|ng-model-rejected="rejFiles"|与不符合通配合而被删除的文件绑定|
|ng-disabled="dropDisabled"|与一个boolean值绑定，来决定是否禁用文件删除功能|
|ngf-change="fileDropped($files, $file, $event, $rejectedFiles)"|当文件被删除时调用|
|ngf-multiple="true" or "false"|默认为false，为true时表示可以选择多个文件|
|ngf-accept="'.pdf,.jpg'"|用逗号分隔允许的MIME类型来过滤文件|

```angular2html
ngf-validate="{
     size: {min: 10, max: '20MB'},
     width: {min: 100, max:10000}, 
     height: {min: 100, max: 300}, 
     duration: {min: '10s', max: '5m'}, 
     accept: '.jpg'
 }" //  或者 "validate($file)"

```

|参数|注释|
|--|--|
|ngf-allow-dir="true" or "false"|默认为true，但只在goole浏览器下可以删除|

```angular2html
ngf-drag-over-class="{
    accept:'acceptClass', 
    reject:'rejectClass', 
    delay:100
}" //or "myDragOverClass" or "calcDragOverClass($event)" 
//拖动css类行为：可以是一个字符串，也可以是一个函数（返回一个类名）或者是一个json对象
{accept: 'c1', reject: 'c2', delay:10}，默认是 "dragover".  accept和reject只可以在chrome浏览器
并且要通过ngf-accept的检测才可以工作，

```

|参数|注释|
|--|--|
|ngf-drop-available="dropSupported"|设置scope模型的值为真或假（基于文件的拖拽和释放）|
|ngf-stop-propagation="true" or "false"|默认为false，是否传播拖拽和释放事件|
|ngf-hide-on-drop-not-available="true" or "false"|默认为false，当文件的拖拽和释放不被支持时隐藏元素|

* 文件预览-----适用于`<img/>`、`<audio>`、`<video>`

|参数|注释|
|--|--|
|ngf-src="file"|通过设置url，预览被选择的文件|
|ngf-background="file"|设置背景图片的样式|
|ngf-no-object-url="true or false"|默认为false，强制生成base64url而不是对象url|

## 参考资料

* [简书教程](http://www.jianshu.com/p/6e14f9200450)
* [ng-file-upload教程](https://www.awesomes.cn/repo/danialfarid/ng-file-upload)
* [CSDN教程](http://blog.csdn.net/csdnmmcl/article/details/51033954)
* [Npm官方介绍](https://www.npmjs.com/package/ng-file-upload)