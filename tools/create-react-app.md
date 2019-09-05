# create-react-app

#### 作者：高天阳
#### 邮箱：13683265113@163.com

```
更改历史

* 2018-09-05        高天阳     初始化文档

```

> create-react-app + antd + react-app-rewired 快速搭建项目环境

## 背景

`Create React App`是FaceBook的React团队官方出的一个构建React单页面应用的脚手架工具。
它本身集成了`Webpack`，并配置了一系列内置的`loader`和默认的npm的脚本，
可以很轻松的实现零配置就可以快速开发React的应用。

## 快速开始

### 全局安装

首先确保你电脑上安装最新的

```
# 全局安装
npm install -g create-react-app
# 构建一个my-app的项目
npx create-react-app my-app
cd my-app

# 启动编译当前的React项目，并自动打开 http://localhost:3000/
npm start
```

以上命令执行完成后，则自动打开： http://localhost:3000/

> 如果你不能确保最新版本，可以先尝试卸载： npm uninstall -g create-react-app,然后再全局安装。

### 构建React项目的其他方式

* npm

```
# npm init <initializer> is available in npm 6+
npm init react-app my-app
```

* Yarn

```
# yarn create is available in Yarn 0.25+
yarn create react-app my-app
```

### 项目目录

项目的默认目录：

```
├── package.json
├── public                  # 这个是webpack的配置的静态目录
│   ├── favicon.ico
│   ├── index.html          # 默认是单页面应用，这个是最终的html的基础模板
│   └── manifest.json
├── src
│   ├── App.css             # App根组件的css
│   ├── App.js              # App组件代码
│   ├── App.test.js
│   ├── index.css           # 启动文件样式
│   ├── index.js            # 启动的文件（开始执行的入口）！！！！
│   ├── logo.svg
│   └── serviceWorker.js
└── package-lock.json
```

### 默认的npm的脚本

#### 启动开发

```
npm start
# or
yarn start
```

#### 启动测试

```
npm test
#or
yarn test
```

#### 构建生产版本

```
npm run build
#or
yarn build
```

#### 解压默认的webpack配置到配置文件中

> 请注意，这个解压步骤是不可逆的，一旦解压，遍无法再次隐藏配置文件
>
> 在这里推荐使用社区开发的react-app-rewired，极大的简化了配置package的步骤

```
npm run eject
```

## 最佳实践

### 引入antd

现在从 yarn 或 npm 安装并引入 antd。

```
npm i antd -D
#or
yarn add antd
```

修改 src/App.js，引入 antd 的按钮组件。

```
import React, { Component } from 'react';
import Button from 'antd/es/button';
import './App.css';

class App extends Component {
  render() {
    return (
      <div className="App">
        <Button type="primary">Button</Button>
      </div>
    );
  }
}

export default App;
```

修改 src/App.css，在文件顶部引入 antd/dist/antd.css。

```
@import '~antd/dist/antd.css';

.App {
  text-align: center;
}

...
```

好了，现在你应该能看到页面上已经有了 antd 的蓝色按钮组件，接下来就可以继续选用其他组件开发应用了。
其他开发流程你可以参考 create-react-app 的
[官方文档。](https://github.com/facebook/create-react-app/blob/master/packages/react-scripts/template/README.md) 

### 高级配置

我们现在已经把组件成功运行起来了，但是在实际开发过程中还有很多问题，
例如上面的例子实际上加载了全部的 antd 组件的样式（gzipped 后一共大约 60kb）。

此时我们需要对 create-react-app 的默认配置进行自定义，
这里我们使用 [react-app-rewired](https://github.com/timarney/react-app-rewired)
（一个对 create-react-app 进行自定义配置的社区解决方案）。

引入 react-app-rewired 并修改 package.json 里的启动配置。
由于新的 [react-app-rewired@2.x](https://github.com/timarney/react-app-rewired#alternatives) 版本的关系，
你还需要安装 [customize-cra](https://github.com/arackaf/customize-cra)。


现在从 yarn 或 npm 安装 react-app-rewired 和 customize-cra。

```
npm i react-app-rewired customize-cra -D
#or
yarn add react-app-rewired customize-cra
```

修改`package.json`

```
"scripts": {
-   "start": "react-scripts start",
+   "start": "react-app-rewired start",
-   "build": "react-scripts build",
+   "build": "react-app-rewired build",
-   "test": "react-scripts test",
+   "test": "react-app-rewired test",
}
```

然后在项目根目录创建一个 `config-overrides.js` 用于修改默认配置。

```
module.exports = function override(config, env) {
  // do stuff with the webpack config...
  return config;
};
```

### 使用 babel-plugin-import

> 注意：antd 默认支持基于 ES module 的 tree shaking，js 代码部分不使用这个插件也会有按需加载的效果。

[babel-plugin-import](https://github.com/ant-design/babel-plugin-import) 是一个用于按需加载组件代码和样式的 babel 插件
（[原理](https://ant.design/docs/react/getting-started-cn#%E6%8C%89%E9%9C%80%E5%8A%A0%E8%BD%BD)），
现在我们尝试安装它并修改 `config-overrides.js` 文件。

```
npm i babel-plugin-import -D
#or
yarn add babel-plugin-import
```

修改`config-overrides.js`

```
+ const { override, fixBabelImports } = require('customize-cra');

- module.exports = function override(config, env) {
-   // do stuff with the webpack config...
-   return config;
- };
+ module.exports = override(
+   fixBabelImports('import', {
+     libraryName: 'antd',
+     libraryDirectory: 'es',
+     style: 'css',
+   }),
+ );
```

然后移除前面在 `src/App.css` 里全量添加的 `@import '~antd/dist/antd.css';` 样式代码，并且按下面的格式引入模块。

> 若不移除此处引用，则修改公共样式无法生效

修改`src/App.js`

```
  import React, { Component } from 'react';
- import Button from 'antd/es/button';
+ import { Button } from 'antd';
  import './App.css';

  class App extends Component {
    render() {
      return (
        <div className="App">
          <Button type="primary">Button</Button>
        </div>
      );
    }
  }

  export default App;
```

最后重启 npm start 访问页面，antd 组件的 js 和 css 代码都会按需加载，
你在控制台也不会看到这样的[警告信息](https://zos.alipayobjects.com/rmsportal/vgcHJRVZFmPjAawwVoXK.png)。
关于按需加载的原理和其他方式可以阅读[这里](https://ant.design/docs/react/getting-started-cn#%E6%8C%89%E9%9C%80%E5%8A%A0%E8%BD%BD)。

### 自定义主题

按照 [配置主题](https://ant.design/docs/react/customize-theme-cn) 的要求，自定义主题需要用到 less 变量覆盖功能。
我们可以引入 `customize-cra` 中提供的 less 相关的函数
[addLessLoader](https://github.com/arackaf/customize-cra#addlessloaderloaderoptions) 来帮助加载 less 样式，
同时修改 `config-overrides.js` 文件如下。

```
npm i less less-loader -D
#or
yarn add less less-loader
```

修改`config-overrides.js`

```
- const { override, fixBabelImports } = require('customize-cra');
+ const { override, fixBabelImports, addLessLoader } = require('customize-cra');

module.exports = override(
  fixBabelImports('import', {
    libraryName: 'antd',
    libraryDirectory: 'es',
-   style: 'css',
+   style: true,
  }),
+ addLessLoader({
+   javascriptEnabled: true,
+   modifyVars: { '@primary-color': '#1DA57A' },
+ }),
);
```

这里利用了 [less-loader](https://github.com/webpack-contrib/less-loader#less-options) 的
`modifyVars` 来进行主题配置，变量和其他配置方式可以参考 [配置主题](https://ant.design/docs/react/customize-theme-cn) 文档。
比如modifyVars的值也可以是一个theme文件。

修改后重启 `npm start`，如果看到一个绿色的按钮就说明配置成功了。

> 你也可以使用 [craco](https://github.com/sharegate/craco) 和
 [craco-antd](https://github.com/DocSpring/craco-antd) 来实现和 customize-cra 一样的修改 create-react-app 配置的功能。

### 关闭sourcemap

打包后我们会发现静态文件夹中会有很多的css和js的map文件，那么我们该怎么关闭sourcemap呢

修改`config-overrides.js`

```
const { override, fixBabelImports, addLessLoader } = require("customize-cra");

+ process.env.GENERATE_SOURCEMAP = "false";

module.exports = override(
  fixBabelImports("import", {
    libraryName: 'antd',
    libraryDirectory: "es",
    style: true,
  }),
  addLessLoader({
    javascriptEnabled: true,
    modifyVars: { '@primary-color': '#1DA57A' },
  })
);
```

再次执行npm run build便不会产生map文件了。

还看到一种解决的方式如下，

```
const rewiredMap = () => config => {
    config.devtool = config.mode === 'development' ? 'cheap-module-source-map' : false;
    return config;
};

module.exports = override(
    // 关闭mapSource
    rewiredMap()
);
```

[详情可看](https://segmentfault.com/q/1010000018123194)

### 本地proxy的配置

开发中常见的问题就是跨域。那么我们前端惯用的方式就是给本地webpack启动的node服务设置代理。

那么具体到使用了新版的cra后，我们该怎么办呢？

很简单，在src目录下新建文件`setupProxy.js`（注意文件名一定要是这个名字，不要问什么，
cra现在废弃了proxy对象配置的方式，将其作为单独模块。解析就是按 src/setupProxy.js这个路径）

安装http代理相关包http-proxy-middleware

```
yarn add http-proxy-middleware -D
```

```
const proxy = require('http-proxy-middleware')

module.exports = function(app) {
  app.use(
    proxy('/api', {
      target: 'http://xx.xx.xx.xx:8000/',
      changeOrigin: true,
      pathRewrite: {
        '^/api': ''
      }
    })
  )
}
```

好了，现在你就可以愉快的访问接口了~

## 同类技术比较

我们要在create-react-app(以下简称cra)中做webpack的配置，有三种方式：

1. 运行npm run eject得到原始的webpack配置文件config，
然后可以看到里面有prod和dev两个环境的相关配置；但是新版本cra你run eject之后，只有一个webpack.config.js文件了。
可以在这里面进行配置。但是本文中这不是我们推荐的方式。

1. 不run eject。而是改写script文件中的js。这个本人没有操作过，这个就不详谈了。

1. 使用react-app-rewired，安装这个工具后，在项目根目录中新建文件config-overrides.js文件。
此时我们便可以在其中进行各种webpack的骚操作了~

**但是！react-app-rewired2.x以后，不再支持injectBabelPlugin的方式，需要安装[customize-cra](https://github.com/arackaf/customize-cra)。**

具体的，ant design官方文档已经给出了最新的解决方案。请[前往详览](https://ant.design/docs/react/use-with-create-react-app-cn)。

因此这种方式就是我们推荐的方式。因为无需生成更多额外的文件，同时配置又趋于更简单可控的方式。

## 参考资料

* [在create-react-app中使用](https://ant.design/docs/react/use-with-create-react-app-cn)
* [create-react-app入门教程](https://www.jianshu.com/p/77bf3944b0f4)
* [关于最新create-react-app使用react-app-rewired2.x添加webpack配置](https://www.cnblogs.com/zyl-Tara/p/10635033.html)

