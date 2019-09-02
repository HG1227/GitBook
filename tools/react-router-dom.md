# react-router-dom

#### 作者：高天阳
#### 邮箱：13683265113@163.com

```
更改历史

* 2019-09-02	    高天阳	初始化文档

```

## 背景

react-router-v4，我称之为“第四代react-router”，react-router和react-router-dom的区别是什么呢？

为什么有时候我们看到如下的写法：

写法1:

```
import {Swtich, Route, Router, HashHistory, Link} from 'react-router-dom';
```
写法2:

```
import {Switch, Route, Router} from 'react-router';
import {HashHistory, Link} from 'react-router-dom';
```

先简单说下各自的功能：

`react-router`: 实现了路由的核心功能

`react-router-dom`: 基于`react-router`，加入了在浏览器运行环境下的一些功能，
例如：`Link`组件，会渲染一个`a`标签，
[Link组件源码`a`标签行](https://github.com/ReactTraining/react-router/blob/master/packages/react-router-dom/modules/Link.js#L76);
 `BrowserRouter`和`HashRouter`组件，前者使用`pushState`和`popState`事件构建路由，
 后者使用`window.location.hash`和`hashchange`事件构建路由。

`react-router-native`: 基于`react-router`，类似`react-router-dom`，加入了`react-native`运行环境下的一些功能。

从源码层面来说明：

首先看`react-router-dom`中的`Switch`组件的源码

```
// Written in this round about way for babel-transform-imports
import { Switch } from 'react-router'
export default Switch
```

只是从`react-router`中导入`Switch`组件，然后重新导出而已。

通过查看其他模块的源码，Route组件的源码、Router组件的源码发现，和`Swtich`一样，都是从`react-router`中导入了相应的组件，
重新导出而已，并没有对实现做什么特殊处理。

结论：

`react-router-dom`依赖`react-router`，所以我们使用`npm`安装依赖的时候，只需要安装相应环境下的库即可，不用再显式安装`react-router`。
基于浏览器环境的开发，只需要安装`react-router-dom`；基于`react-native`环境的开发，只需要安装`react-router-native`。
`npm`会自动解析`react-router-dom`包中`package.json`的依赖并安装。

`react-router-dom`中`package.json`依赖:

```
"dependencies": {
    "history": "^4.7.2",
    "invariant": "^2.2.2",
    "loose-envify": "^1.3.1",
    "prop-types": "^15.5.4",
    "react-router": "^4.2.0",
    "warning": "^3.0.0"
  }
```

安装了`react-router-dom`，`npm`会解析并安装上述依赖包。可以看到，其中包括`react-router`。

所以，回到最开始的写法。基于浏览器环境的开发，写法1就可以了。

## 参考资料

* [react-router和react-router-dom的区别](https://blog.csdn.net/weixin_37242696/article/details/80738392)
* [ReactTraining/react-router#4648](https://github.com/ReactTraining/react-router/issues/4648)
* [react-router README](https://github.com/ReactTraining/react-router/blob/master/packages/react-router/README.md)


