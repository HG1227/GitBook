# GitBook

#### 作者：高天阳&王志伟

```angular2html
文档须知
* 2018-10-17	高天阳	尝试修复插件无法推送123
* 2018-02-12	王志伟	补充资料
* 2017-06-29    高天阳	初始化项目
```

## 1 概述

本项目文档:[Gitbook链接地址](https://mitudegaoyang.gitbooks.io/mybook/content/)，

Gitbook详细说明见:[Gitbook的使用](TraingRecord/GitBook.md)
markdown详细说明见:[Markdown](TraingRecord/markdown.md)
文档书写规范:[培训材料撰写](TraingRecord/TrainingMaterialWriting.md)

## 2 使用

### 2.1 安装

```bash
# 克隆项目
$ git clone git@github.com:mitudegaoyang/GitBook.git

# 安装gitbook
$ npm install gitbook -g

# 安装gitbook脚手架
$ npm install gitbook-cli -g

# 检测是否安装成功
$ gitbook --version
```

### 2.2 常用指令

```bash
# 初始化
$ gitbook init

# 本地预览
$ gitbook serve

# 编译书籍
$ gitbook build
```

## 3 开发

### 3.1 目录结构

```
- README.md     #项目说明
- SUMMARY.md    #项目目录
- assets        #图片存储目录
```

### 其它

test

## 4 常见问题

### 4.1 推送权限不足

设置remotes为https格式

#### 添加远程仓库(https格式)

复制仓库http格式

![](assets/githubClone.jpeg)

设置webstorm的gitRemotes为https模式

![](assets/webstormChange.png)
![](assets/webstormChange2.png)

再次执行push

## 参考

* [webstorm 推送项目到github](https://blog.csdn.net/mjth2014/article/details/80256224)