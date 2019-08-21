# Webpack

# webpack2 培训 {#webpack2-培训}

### 第一章 webpack介绍 {#第一章-webpack介绍}

#### 1.1 概述 {#11-概述}

Webpack 是当下最热门的前端资源模块化管理和打包工具。它可以将许多松散的模块按照依赖和规则打包成符合生产环境部署的前端资源。
还可以将按需加载的模块进行代码分隔，等到实际需要的时候再异步加载。通过 loader 的转换，任何形式的资源都可以视作模块，
比如 CommonJs 模块、 AMD 模块、 ES6 模块、CSS、图片、 JSON、Coffeescript、 LESS 等。

### 第二章 安装 {#第二章-安装}

#### 2.1 前提条件 {#21-前提条件}

在开始前，先要确认你已经安装[Node.js](https://nodejs.org/en/)的最新版本。使用 Node.js 最新的 LTS 版本，是理想的启动入口。
使用旧版本，你可能遇到各种问题，因为它们可能缺少 webpack 功能或缺少相关 package 包。

#### 2.2 安装 {#22-安装}

1. 创建一个文件夹，npm初始化，本地安装webpack

```
mkdir webpack-demo && cd webpack-demo
npm init -y
npm install --save-dev webpack
```

2.创建如下的目录结构和文件

**project**

```
  webpack-demo
    |- package.json
  + |- index.html
  + |- /src
  + |- index.js
```

**src/index.js**

```
function component() {
  var element = document.createElement('div');

  // 需要引入 lodash，下一行才能正常工作
  element.innerHTML = _.join(['Hello', 'webpack'], ' ');

  return element;
}

document.body.appendChild(component());

```

**index.html**

```
<html>
    <head>
        <title>Getting Started</title>
        <script src="https://unpkg.com/lodash@4.16.6"></script>
    </head>
    <body>
        <script src="./src/index.js"></script>
    </body>
</html>
```

### 第三章 创建一个 bundle 文件 {#第三章-创建一个-bundle-文件}

首先我们稍微调整我们的目录结构，将源代码（src）与我们的目标代码（dist）分开。“源”代码是我们将编写和编辑的代码。
“目标”代码是`output`最终将最终加载到浏览器中的构建过程的最优化的代码。

**project**

```
  webpack-demo
  |- package.json
+ |- /dist
+ |- index.html
- |- index.html
  |- /src
  |- index.js

```

在`index.js`中打包`lodash`依赖，首先我们需要安装`lodash`。

```
npm install --save lodash
```

然后 import lodash。

**src/index.js**

```
+ import _ from 'lodash';
+
  function component() {
    var element = document.createElement('div');

-   // Lodash, currently included via a script, is required for this line to work
+   // Lodash, now imported by this script
    element.innerHTML = _.join(['Hello', 'webpack'], ' ');

    return element;
  }

  document.body.appendChild(component());

```

我们还要修改dist下的`index.html`，来引入按照预期打包的单个 js 文件。

```
<html>
   <head>
     <title>Getting Started</title>
-    <script src="https://unpkg.com/lodash@4.16.6"></script>
   </head>
   <body>
-    <script src="./src/index.js"></script>
+    <script src="bundle.js"></script>
   </body>
</html>
```

这里，`index.js`显式要求引入的`lodash`必须存在，然后将它以`_`的别名绑定（不会造成全局范围变量名污染）。

通过展示出模块所需依赖，webpack 能够利用这些信息去构建依赖图表。然后 webpack 使用图表生成一个优化过的 bundle，脚本还将以正确的顺序执行。并且没有用到的依赖将不会被 bundle 引入。

现在在此文件夹下运行`webpack`，其中`index.js`是输入文件，`bundle.js`是输出文件，输出文件已打包此页面所需的所有代码。

```
webpack app/index.js dist/bundle.js

Hash: ff6c1d39b26f89b3b7bb
Version: webpack 2.2.0
Time: 385ms
    Asset    Size  Chunks                    Chunk Names
bundle.js  544 kB       0  [emitted]  [big]  main
   [0] ./~/lodash/lodash.js 540 kB {0} [built]
   [1] (webpack)/buildin/global.js 509 bytes {0} [built]
   [2] (webpack)/buildin/module.js 517 bytes {0} [built]
   [3] ./app/index.js 278 bytes {0} [built]

```

在浏览器中打开`index.html`，查看成功后 bundle 的结果。 你应该看到带有以下文本的页面：'Hello webpack'。

### 第四章 使用带有配置的 webpack {#第四章-使用带有配置的-webpack}

对于更复杂的配置，我们可以使用配置文件，webpack 会引用它来打包代码。然后创建一个`webpack.config.js`文件，你可以使用以下配置表示上述 CLI 命令。

**project**

```
  webpack-demo
  |- package.json
+ |- webpack.config.js
  |- /dist
  |- index.html
  |- /src
  |- index.js

```

**webpack.config.js**

```
const path = require('path');

module.exports = {
  entry: './src/index.js',
  output: {
    filename: 'bundle.js',
    path: path.resolve(__dirname, 'dist')
  }
};

```

_其中_`entry`_是指页面中的入口文件。也就是打包从哪个文件开始。_

`output`_项告诉webpack怎样存储输出结果以及存储到哪里。_

此文件可以由接下来的 webpack 命令运行。

```
webpack --config webpack.config.js

Hash: ff6c1d39b26f89b3b7bb
Version: webpack 2.2.0
Time: 390ms
    Asset    Size  Chunks                    Chunk Names
bundle.js  544 kB       0  [emitted]  [big]  main
   [0] ./~/lodash/lodash.js 540 kB {0} [built]
   [1] (webpack)/buildin/global.js 509 bytes {0} [built]
   [2] (webpack)/buildin/module.js 517 bytes {0} [built]
   [3] ./src/index.js 278 bytes {0} [built]

```

### 第五章 使用引入 npm 的 webpack {#第五章-使用引入-npm-的-webpack}

考虑到用 CLI 这种方式来运行 webpack 不是特别方便，我们可以设置一个快捷方式。像这样调整

_package.json_

```
{
  ...
  "scripts": {
    "build": "webpack"
  },
  ...
}

```

现在你可以通过使用`npm run build`命令来实现与上面相同的效果。npm 通过命令选取脚本，并临时修补执行环境，使脚本可以在运行时包含 bin 命令。你可以看到很多项目都如此约定。

### 第六章 静态资源管理 {#第六章-静态资源管理}

webpack这样的工具会动态地捆绑所有依赖关系（创建所谓的依赖图）。这是非常好的，因为每个模块现在明确说明其依赖关系，我们将避免捆绑未使用的模块。

最酷的webpack功能之一是除了JavaScript之外，还可以包含任何其他类型的文件，其中有一个加载程序。

#### 6.1 载入CSS {#61-载入css}

为了将CSS文件`import`JavaScript模块，您需要安装并将style-loader和css-loader添加到您的module配置中

```
npm install --save-dev style-loader css-loader

```

**webpack.config.js**

```
const path = require('path');

  module.exports = {
    entry: './src/index.js',
    output: {
      filename: 'bundle.js',
      path: path.resolve(__dirname, 'dist')
    },
+   module: {
+     rules: [
+       {
+         test: /\.css$/,
+         use: [
+           'style-loader',
+           'css-loader'
+         ]
+       }
+     ]
+   }
  };

```

_webpack使用正则表达式来确定应该查找哪些文件并将其提供给特定的加载程序。在这种情况下，任何结尾的文件.css将被提供给style-loader和css-loader。_

让我们尝试通过style.css在我们的项目中添加一个新文件，并将其导入到我们的index.js

**project**

```
 webpack-demo
  |- package.json
  |- webpack.config.js
  |- /dist
    |- bundle.js
    |- index.html
  |- /src
+   |- style.css
    |- index.js
  |- /node_modules

```

**src/style.css**

```
.hello {
  color: red;
}

```

**src/index.js**

```
  import _ from 'lodash';
+ import './style.css';

  function component() {
    var element = document.createElement('div');

    // Lodash, now imported by this script
    element.innerHTML = _.join(['Hello', 'webpack'], ' ');
+   element.classList.add('hello');

    return element;
  }

  document.body.appendChild(component());

```

运行一个新的构建

```
npm run build

Hash: 854865050ea3c1c7f237
Version: webpack 2.6.1
Time: 895ms
                               Asset     Size  Chunks                    Chunk Names
5c999da72346a995e7e2718865d019c8.png  11.3 kB          [emitted]
                           bundle.js   561 kB       0  [emitted]  [big]  main
   [0] ./src/icon.png 82 bytes {0} [built]
   [1] ./~/lodash/lodash.js 540 kB {0} [built]
   [2] ./src/style.css 1 kB {0} [built]
   [3] ./~/css-loader!./src/style.css 242 bytes {0} [built]
   [4] ./~/css-loader/lib/css-base.js 2.26 kB {0} [built]
   [5] ./~/style-loader/lib/addStyles.js 8.7 kB {0} [built]
   [6] ./~/style-loader/lib/urls.js 3.01 kB {0} [built]
   [7] (webpack)/buildin/global.js 509 bytes {0} [built]
   [8] (webpack)/buildin/module.js 517 bytes {0} [built]
   [9] ./src/index.js 503 bytes {0} [built]

```

再次在浏览器中打开`index.html`，您应该看到`Hello webpack`现在是红色样式。

### 6.2 加载图像 {#62-加载图像}

使用文件加载器，我们可以很容易地将图像如背景和图标加载在我们的系统中：  
`npm install --save-dev file-loader`  
**webpack.config.js**

```
  module.exports = {
    entry: './src/index.js',
    output: {
      filename: 'bundle.js',
      path: path.resolve(__dirname, 'dist')
    },
    module: {
      rules: [
        {
          test: /\.css$/,
          use: [
            'style-loader',
            'css-loader'
          ]
        },
+       {
+         test: /\.(png|svg|jpg|gif)$/,
+         use: [
+           'file-loader'
+         ]
+       }
      ]
    }
  };

```

让我们向项目添加一个图像，看看它是如何工作的  
**project**

```
  webpack-demo
  |- package.json
  |- webpack.config.js
  |- /dist
  |- bundle.js
  |- index.html
  |- /src
+ |- icon.png
  |- style.css
  |- index.js
  |- /node_modules

```

**src/index.js**

```
  import _ from 'lodash';
  import './style.css';
+ import Icon from './icon.png';

  function component() {
    var element = document.createElement('div');

    // Lodash, now imported by this script
    element.innerHTML = _.join(['Hello', 'webpack'], ' ');
    element.classList.add('hello');

+   // Add the image to our existing div.
+   var myIcon = new Image();
+   myIcon.src = Icon;
+
+   element.appendChild(myIcon);

    return element;
  }
  document.body.appendChild(component());

```

**src/style.css**

```
  .hello {
    color: red;
+   background: url('./icon.png');
  }

```

现在运行你的构建命令：

```
npm run build

Hash: 854865050ea3c1c7f237
Version: webpack 2.6.1
Time: 895ms
                               Asset     Size  Chunks                    Chunk Names
5c999da72346a995e7e2718865d019c8.png  11.3 kB          [emitted]
                           bundle.js   561 kB       0  [emitted]  [big]  main
   [0] ./src/icon.png 82 bytes {0} [built]
   [1] ./~/lodash/lodash.js 540 kB {0} [built]
   [2] ./src/style.css 1 kB {0} [built]
   [3] ./~/css-loader!./src/style.css 242 bytes {0} [built]
   [4] ./~/css-loader/lib/css-base.js 2.26 kB {0} [built]
   [5] ./~/style-loader/lib/addStyles.js 8.7 kB {0} [built]
   [6] ./~/style-loader/lib/urls.js 3.01 kB {0} [built]
   [7] (webpack)/buildin/global.js 509 bytes {0} [built]
   [8] (webpack)/buildin/module.js 517 bytes {0} [built]
   [9] ./src/index.js 503 bytes {0} [built]

```

#### 6.3 加载字体 {#toc_0}

**webpack.config.js**

```
const path = require('path');

  module.exports = {
    entry: './src/index.js',
    output: {
      filename: 'bundle.js',
      path: path.resolve(__dirname, 'dist')
    },
    module: {
      rules: [
        {
          test: /\.css$/,
          use: [
            'style-loader',
            'css-loader'
          ]
        },
        {
          test: /\.(png|svg|jpg|gif)$/,
          use: [
            'file-loader'
          ]
        },
+       {
+         test: /\.(woff|woff2|eot|ttf|otf)$/,
+         use: [
+           'file-loader'
+         ]
+       }
      ]
    }
  };

```

**project**

```
 webpack-demo
  |- package.json
  |- webpack.config.js
  |- /dist
    |- bundle.js
    |- index.html
  |- /src
+   |- my-font.woff
+   |- my-font.woff2
    |- icon.png
    |- style.css
    |- index.js
  |- /node_modules

```

**src/style.css**

```
+ @font-face {
+   font-family: 'MyFont';
+   src:  url('./my-font.woff2') format('woff2'),
+         url('./my-font.woff') format('woff');
+   font-weight: 600;
+   font-style: normal;
  }

  .hello {
    color: red;
+   font-family: 'MyFont';
    background: url('./icon.png');
  }

```

现在运行一个新的构建，让我们看看webpack是否处理了我们的字体

```
npm run build

Hash: b4aef94169088c79ed1c
Version: webpack 2.6.1
Time: 775ms
                                Asset     Size  Chunks                    Chunk Names
 5c999da72346a995e7e2718865d019c8.png  11.3 kB          [emitted]
11aebbbd407bcc3ab1e914ca0238d24d.woff   221 kB          [emitted]
                            bundle.js   561 kB       0  [emitted]  [big]  main
   [0] ./src/icon.png 82 bytes {0} [built]
   [1] ./~/lodash/lodash.js 540 kB {0} [built]
   [2] ./src/style.css 1 kB {0} [built]
   [3] ./~/css-loader!./src/style.css 420 bytes {0} [built]
   [4] ./~/css-loader/lib/css-base.js 2.26 kB {0} [built]
   [5] ./src/MyFont.woff 83 bytes {0} [built]
   [6] ./~/style-loader/lib/addStyles.js 8.7 kB {0} [built]
   [7] ./~/style-loader/lib/urls.js 3.01 kB {0} [built]
   [8] (webpack)/buildin/global.js 509 bytes {0} [built]
   [9] (webpack)/buildin/module.js 517 bytes {0} [built]
  [10] ./src/index.js 503 bytes {0} [built]

```

再次打开index.html，看看我们的Hello webpack文字是否已经变成了新的字体。如果一切顺利，您应该看到更改。

### 第七章 webpack-dev-server {#toc_1}

`webpack-dev-server`是一个小型的Node.js Express服务器,它使用`webpack-dev-middleware`来服务于webpack的包,除此自外，它还有一个通过Sock.js来连接到服务器的微型运行时.  
`webpack-dev-server`是一个独立的NPM包,你可以通过`npm install webpack-dev-server`来安装它.

#### 6.1 基本目录 {#toc_2}

webpack-dev-server默认会以当前目录为基本目录,除非你制定它

```
webpack-dev-server --content-base build/

```

上述命令是在命令行中执行的,它将build目录作为根目录.有一点需要注意的是:webpack-dev-server生成的包并没有放在你的真实目录中,而是放在了内存中.

在浏览器中输入[http://localhost:8080](http://localhost:8080/)访问

#### 6.2 自动刷新 {#toc_3}

webpack-dev-server支持两种模式来自动刷新页面.

* iframe模式\(页面放在iframe中,当发生改变时重载\)
* inline模式\(将webpack-dev-sever的客户端入口添加到包\(bundle\)中\) 两种模式都支持热模块替换\(Hot Module Replacement\).热模块替换的好处是只替换更新的部分,而不是页面重载.

在命令行中运行inline模式，并启用热模块替换  
这里只需要多增加 --hot指令就OK了.如下所示.

`webpack-dev-server --content-base build --inline --hot`
