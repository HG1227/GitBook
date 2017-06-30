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

`webpack 目标文件 打包后文件名 需要执行的loader`

`webpack hello.js hello.bundle.js --module-bind "css=style-loader!css-loader`

![](/assets/webpack5.png)
