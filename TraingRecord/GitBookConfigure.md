# GitBook更多配置

#### 作者：高天阳
#### 邮箱：13683265113@163.com

```
更改历史

* 2019-07-24	    高天阳	初始化文档
```

## 全局配置

配置根目录下book.json文件

### title 设置书本的标题

`“title” : “私人笔记”`

### author 作者的相关信息

`“author” : “gaotianyang”`

### description 本书的简单描述

`“description” : “gaotianyang的私人笔记”`

### language Gitbook使用的语言

版本2.6.4中可选的语言如下：

en, ar, bn, cs, de, en, es, fa, fi, fr, he, it, ja, ko, no, pl, pt, ro, ru, sv, uk, vi, zh-hans, zh-tw

例如，配置使用简体中文

`“language” : “zh-hans”`

### links 在左侧导航栏添加链接信息

```json
{
    "links": {
        "sidebar": {
            "Home": "https://www.baidu.com"
        }
    }
}
```

### styles 自定义页面样式

```json
{
    "styles": {
        "website": "styles/website.css",
        "ebook": "styles/ebook.css",
        "pdf": "styles/pdf.css",
        "mobi": "styles/mobi.css",
        "epub": "styles/epub.css"
    }
}
```

例如使`h1 h2`标签有下划线， 可以在`website.css`中设置

```css
h1 , h2{
    border-bottom: 1px solid #EEEEEE;
}
```

## plugins 插件列表

### 配置使用的插件

```json
{
    "plugins": [
        "-search",
        "back-to-top-button",
        "expandable-chapters-small",
        "insert-logo"
    ]
}
```

其中`"-search"`中的 `-` 符号代表去除默认自带的插件

Gitbook默认自带有5个插件：

* highlight：代码高亮
* search：导航栏查询功能（不支持中文）
* sharing：右上角分享功能
* font-settings：字体设置（最上方的"A"符号）
* livereload：为GitBook实时重新加载

### 插件属性配置pluginsConfig

配置插件的属性

例如配置`insert-logo`的属性：

```json
{
    "pluginsConfig": {
        "insert-logo": {
            "url": "images/logo.png",
            "style": "background: none; max-height: 30px; min-height: 30px"
        }
    }
}
```

## 一些实用插件

记录一些实用的插件

用法：在book.json中添加以下内容。然后执行`gitbook install`，
或者使用NPM安装（单独安装推荐NPM）`npm install gitbook-plugin-插件名`，
也可以从源码GitHub地址中下载，放到`node_modules`文件夹里（GitHub地址在进入插件地址右侧的GitHub链接）

### back-to-top-button 回到顶部

[GitHub地址](https://github.com/stuebersystems/gitbook-plugin-back-to-top-button)

在book.json中添加以下内容。然后执行`gitbook install`，
或者使用NPM安装（单独安装推荐NPM）`npm install gitbook-plugin-back-to-top-button`，
也可以从源码GitHub地址中下载，放到`node_modules`文件夹里（GitHub地址在进入插件地址右侧的GitHub链接）

```json
{
    "plugins": [
         "back-to-top-button"
    ]
}
```

### 导航目录折叠

#### chapter-fold 左侧目录折叠

支持多层目录，点击导航栏的标题名就可以实现折叠扩展。

[GitHub地址](https://github.com/ColinCollins/gitbook-plugin-chapter-fold)

在book.json中添加以下内容。然后执行`gitbook install`，
或者使用NPM安装（单独安装推荐NPM）`npm install gitbook-plugin-chapter-fold`，
也可以从源码GitHub地址中下载，放到`node_modules`文件夹里（GitHub地址在进入插件地址右侧的GitHub链接）

```json
{
    "plugins": [
         "chapter-fold"
    ]
}
```

#### expandable-chapters-small 左侧章节目录可折叠

支持多层目录，比Toggle Chapters好用 只有点击箭头才能实现折叠扩展。不如【2.2.1. chapter-fold 左侧目录折叠】好用

[GitHub地址](https://github.com/chrisjake/gitbook-plugin-expandable-chapters-small)

在book.json中添加以下内容。然后执行`gitbook install`，
或者使用NPM安装（单独安装推荐NPM）`npm install gitbook-plugin-expandable-chapters-small`，
也可以从源码GitHub地址中下载，放到`node_modules`文件夹里（GitHub地址在进入插件地址右侧的GitHub链接）

```json
{
    "plugins": [
         "expandable-chapters-small"
    ]
}
```

#### expandable-chapters 可扩展导航章节

和expandable-chapters-small效果相同，唯一不同的是这个插件的箭头粗

[GitHub地址](https://github.com/DomainDrivenArchitecture/gitbook-plugin-expandable-chapters)

在book.json中添加以下内容。然后执行`gitbook install`，
或者使用NPM安装（单独安装推荐NPM）`npm install gitbook-plugin-expandable-chapters`，
也可以从源码GitHub地址中下载，放到`node_modules`文件夹里（GitHub地址在进入插件地址右侧的GitHub链接）

```json
{
    "plugins": [
         "expandable-chapters"
    ]
}
```

### 代码复制，行号

#### code 代码添加行号&复制按钮（可选）

为代码块添加行号和复制按钮，复制按钮可关闭

单行代码无行号。

[GitHub地址](https://github.com/TGhoul/gitbook-plugin-code)

在book.json中添加以下内容。然后执行`gitbook install`，
或者使用NPM安装（单独安装推荐NPM）`npm install gitbook-plugin-code`，
也可以从源码GitHub地址中下载，放到`node_modules`文件夹里（GitHub地址在进入插件地址右侧的GitHub链接）

```json
{
    "plugins": [
         "code"
    ]
}
```

如果想去掉复制按钮，在book.json的插件配置块更新：

```json
{
    "plugins" : [ "code" ],
    "pluginsConfig": {
          "code": {
          "copyButtons": false
      }
    }
}
```

#### copy-code-button 代码块复制按钮

为代码块添加复制的按钮。

在book.json中添加以下内容。然后执行`gitbook install`，
或者使用NPM安装（单独安装推荐NPM）`npm install gitbook-plugin-copy-code-button`，
也可以从源码GitHub地址中下载，放到`node_modules`文件夹里（GitHub地址在进入插件地址右侧的GitHub链接）

```json
{
    "plugins": [
         "copy-code-button"
    ]
}
```

效果如下图所示

![](../assets/gitbook/copy-code-button.png)

### todo 待做项☑

添加 Todo 功能。默认的 checkbox 会向右偏移 2em，如果不希望偏移，可以在 `website.css` 里加上下面的代码:

```css
input[type=checkbox]{
    margin-left: -2em;
}
```

[GitHub地址](https://github.com/ly-tools/gitbook-plugin-todo)

在book.json中添加以下内容。然后执行`gitbook install`，
或者使用NPM安装（单独安装推荐NPM）`npm install gitbook-plugin-todo`，
也可以从源码GitHub地址中下载，放到`node_modules`文件夹里（GitHub地址在进入插件地址右侧的GitHub链接）

```json
{
    "plugins": ["todo"]
}
```

使用示例：

```
*   [ ]  write some articles
*   [x]  drink a cup of tea
```

### 其他：设置导航序号

配置，可以在book.json的pluginsConfig中添加如下：

```json
{
    "pluginsConfig": {
        "theme-default": {
        "showLevel": true
        }
    }
}
```

## 配置示例

```json
{
    "title": "G笔记",
    "description": "好记性不如G笔记",
    "author": "lijiam",
    "output.name": "site",
    "language": "zh-hans",
    "gitbook": "3.2.3",
    "root": ".",
    "links": {
        "sidebar": {
            "首页": "http://www.lijiam.com"
        }
    },
    "plugins": [
        "code",
        "-search",
        "search-pro",
        "github",
        "splitter",
        "tbfed-pagefooter",
        "donate",
        "-sharing",
        "sharing-plus",
        "prism",
        "-highlight",
        "styles-less",
        "toggle-chapters",
        "multipart",
        "ancre-navigation"
    ],
    "pluginsConfig": {
        "github": {
            "url": "https://github.com/lijiam"
        },
        "code": {
            "copyButtons": true
        },
        "tbfed-pagefooter": {
            "copyright": "Copyright © lijiam 2019",
            "modify_label": "本书发布时间：",
            "modify_format": "YYYY-MM-DD HH:mm:ss"
        },
        "donate": {
            "wechat": "/assets/images/wxpay.png",
            "alipay": "/assets/images/alipay.png",
            "title": "",
            "button": "赏",
            "alipayText": "支付宝打赏",
            "wechatText": "微信打赏"
        },
        "sharing": {
            "facebook": true,
            "twitter": true,
            "weibo": true,
            "qq": true,
            "all": [
                "douban",
                "google",
                "qzone",
                "linkedin"
            ]
        },
        "prism": {
            "css": [
                "prismjs/themes/prism-solarizedlight.css"
            ],
            "lang": {
                "flow": "typescript"
            }
        }
    },
    "styles": {
        "website": "assets/styles/website.less",
        "ebook": "assets/styles/ebook.less",
        "pdf": "assets/styles/pdf.less",
        "mobi": "assets/styles/mobi.less",
        "epub": "assets/styles/epub.less"
    }
}
```

## 参考资料

* [GitBook插件整理 - book.json配置](https://www.cnblogs.com/mingyue5826/p/10307051.html)
* [gitbook的插件配置](https://www.cnblogs.com/yonguo123/p/9524024.html)
* [gitbook安装与使用](https://blog.csdn.net/fghsfeyhdf/article/details/88403548)
* [gitbook常用插件简介](https://blog.csdn.net/qq_37149933/article/details/64170653)
* [gitbook安装代码高亮插件：Prism](https://www.crifan.com/gitbook_install_code_highlight_plugin_prism/)
* [gitbook菜单序号设置](https://www.crifan.com/gitbook_add_chapter_index_number/)