# 关于Webpack的学习记录

## webpack基本介绍

### webpack安装

* 创建目录并初始化

`mkdir 文件夹名`

`cd 文件夹`

* 安装开发依赖

`yarn add webpack --dev`

* 安装项目css-loader、style-loader依赖

`yarn add css-loader style-loader --dev`

## webpack使用流程

* 创建项目文件

html、js、css

![](/assets/webpack/webpack1.png)  
![](/assets/webpack/webpack2.png)  
![](/assets/webpack/webpack3.png)  
![](/assets/webpack/webpack4.png)

注意:引用方式为require

* 打包项目

`webpack 目标文件 打包后文件名 需要执行的参数`

`--module-bind模块绑定参数`

`webpack hello.js hello.bundle.js --module-bind "css=style-loader!css-loader"`

`--watch监听参数`

`webpack hello.js hello.bundle.js --module-bind "css=style-loader!css-loader" --watch`

`--progress查看打包过程参数`

`webpack hello.js hello.bundle.js --module-bind "css=style-loader!css-loader" --progress`

`--display-modules查看打包模块参数`

`webpack hello.js hello.bundle.js --module-bind "css=style-loader!css-loader" --progress --display-modules`

`--display-reasons查看打包模块原因参数`

`webpack hello.js hello.bundle.js --module-bind "css=style-loader!css-loader" --progress --display-modules --display-reasons`

![](/assets/webpack/webpack5.png)

## webpack基本配置

### webpack项目的从零构建

* 创建目录并初始化
* 安装开发依赖

`yarn add webpack --dev`

* 创建项目文件html、js、css

![](/assets/webpack/webpack6.png)

* 编辑webpack.config.js配置文件

![](/assets/webpack/webpack7.png)

* 运行webpack命令

`webpack`

目录结构发生改变 在规定位置生成bundle.js文件

![](/assets/webpack/webpack8.png)

### webpack配置的entry和output

webpack.config.js文件entry的3种形式

* 字符串

![](/assets/webpack/webpack9.png)

* 数组

![](/assets/webpack/webpack10.png)

* 对象

注意:由于多个单独模块都必须只有唯一名称  
因此需要按下图方式修改output来确保输出的唯一性

![](/assets/webpack/webpack11.png)

此处的`[name][hash][chunkhash]`分别为

![](/assets/webpack/webpack12.png)

## 生成项目中的html页面文件

### 自动化生成项目中的html并对打包后的js自动引入

注意:此处的path不可省略并必须严格加上`__dirname`并且在目录结构处必须写成`/dist/`才能找到
另外值得注意的是,生成的js、html均在`dist/js`文件夹下

![](/assets/webpack/webpack13.png)

如果希望生成的html按照我们期望的格式生成可以给插件添加参数

![](/assets/webpack/webpack14.png)

## 处理项目中的资源文件