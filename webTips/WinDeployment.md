# Windows部署时脚本报错

## 1.报错信息

在执行部署脚本时 出现以下错误

![](/assets/WinDeployment1.png)

## 2.报错原因

Windows环境下 不支持异步上传命令

## 3.解决方案

部署脚本的原理就是向服务器发送项目压缩包
 
WinSCP软件 同样可以往服务器以拖拽的形式上传 相当于ftp上传

![](/assets/WinDeployment2.jpeg)

## 4.使用方法

### 4.1创建与服务器链接

![](/assets/WinDeployment3.jpeg)

### 4.2打开项目打包文件目录及服务器部署目录

![](/assets/WinDeployment4.jpeg)

> 以某项目为例 将dist文件夹下所有内容拖拽至服务器data/v1目录下

![](/assets/WinDeployment5.jpeg)

![](/assets/WinDeployment6.jpeg)