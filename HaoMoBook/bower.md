# bower培训 {#bower培训}

> 常用命令说明

* bower初始化

```
bower init
```

* 查看插件是否存在于bower库

```
bower search [插件名称]
```

* 安装插件并存储于项目依赖

```
bower install [插件名称] --save

bower install [插件名称] -S
```

安装插件并存储于开发依赖

```
bower install [插件名称] --save-dev


bower install [插件名称] -D
```

## 第一章 bower简介 {#第一章-bower简介}

## 第二章 bower安装使用 {#第一章-bower安装使用}

### 1.1 bower安装 {#11-bower安装}

bower是基于nodeJS的前端包管理工具，bower需要远程git仓库获得资源，故而bower的安装应当具备：

* node
* npm
* git

bower的安装：

```
npm install bower -g          #-g表示全局安装
```

### 1.2 bower使用 {#12-bower使用}

* bower init

项目目录下，使用bower init创建bower.json文件

```
bower init
```

* bower install

```
bower install [
<
options
>
]
bower install 
<
endpoint
>
 [
<
endpoint
>
 ..] [
<
options
>
]
```

这个指令将递归安装项目所需依赖；

其中endpoint可以是：

> * 一个package的名字例如:jquery，lodash..
> * 一个git端点例如: git@github.com:user/package.git或者
>   [https://github.com/user/package.git](https://github.com/user/package.git)
> * 一个文件地址

等等

option指的是：

> * -F/--force-latest 强制安装最新版本的package
> * --p/--production 不要安装项目依赖的devDependencies
> * -S/--save 将下载的安装包安装到bower.json的dependencies中
> * -D/--save-dev 将下载的安装包安装到bower.json的devDependencies中
> * -E/--save-exact 配置下载一个制定版本的package，而不是项目中必须依赖的版本

* bower list

bower list可以查看当前目录下已安装的package以及可能的版本更新信息

* bower lookup

查看pkg的url；

* bower update

```
bower update 
<
pkg
>
```

将bower升级到最新的版本

* bower uninstall

```
bower uninstall 
<
pkg
>
```

删除特定的 package；

* bower cache

```
bower cache list
bower cache clean
```

### 2.3配置bower下载package的安装路径 {#23配置bower下载package的安装路径}

创建.bowerrc文件:

```
{
  "directory": "app/dist"
}
```

配置这个选项，会将bower下载的安装包下载到app/dist目录下取代默认的bower\_components路径

## 参考文档 {#参考文档}

* bower官方文档：
  [https://bower.io/docs/api/](https://bower.io/docs/api/)
* .bowerrc配置文档：
  [https://github.com/bower/spec/blob/master/config.md](https://github.com/bower/spec/blob/master/config.md)



