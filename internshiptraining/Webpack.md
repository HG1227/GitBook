# 关于Webpack的学习记录

## 安装流程
1. 创建目录并初始化

`mkdir 文件夹名`

`cd 文件夹`

2. 安装开发依赖

`yarn add webpack --dev`

3. 安装项目css-loader、style-loader依赖

`yarn add css-loader style-loader --dev`

## 使用流程
4. 创建项目文件

html、js、css

![](/assets/webpack1.png)
![](/assets/webpack2.png)
![](/assets/webpack3.png)
![](/assets/webpack4.png)

注意:引用方式为require

5. 打包项目

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

![](/assets/webpack5.png)

## webpack项目的从零构建

1. 创建目录并初始化
2. 安装开发依赖

`yarn add webpack --dev`

3. 创建项目文件html、js、css

![](/assets/webpack6.png)

4. 编辑webpack.config.js配置文件

![](/assets/webpack7.png)

5. 运行webpack命令

`webpack`

目录结构发生改变 在规定位置生成bundle.js文件

![](/assets/webpack8.png)
