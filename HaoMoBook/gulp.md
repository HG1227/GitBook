# gulp培训 {#gulp培训}

## 第一章 gulp介绍 {#第一章-gulp介绍}

### 1.1 gulp简介 {#11-gulp简介}

在现在的前端开发中，前后端分离、模块化开发、版本控制、文件合并与压缩、mock数据等等一些原本后端的思想开始逐渐渗透到“大前端”的开发中。前端开发过程越来越繁琐，当今越来越多的网站已经从网页模式进化到了 Webapp 模式。它们运行在现代的高级浏览器里，使用 HTML5、 CSS3、 ES6 等更新的技术来开发丰富的功能，网页已经不仅仅是完成浏览的基本需求，并且Webapp通常是一个单页面应用\(SPA\)，每一个视图通过异步的方式加载，这导致页面初始化和使用过程中会加载越来越多的 JavaScript 代码，这给前端开发的流程和资源组织带来了巨大的挑战。

前端开发和其他开发工作的主要区别，首先是前端是基于多语言、多层次的编码和组织工作，其次前端产品的交付是基于浏览器，这些资源是通过增量加载的方式运行到浏览器端，如何在开发环境组织好这些碎片化的代码和资源，并且保证他们在浏览器端快速、优雅的加载和更新，就需要一个模块化系统，

gulp是前端开发过程中一种基于流的 代码构建工具 ，是自动化项目的构建利器；它不仅能对网站资源进行优化，而且在开发过程中很多重复的任务能够使用正确的工具自动完成；使用它，不仅可以很愉快的编写代码，而且大大提高我们的工作效率。

### 1.2 类似工具 {#12-类似工具}

**grunt**Grunt是基于Node.js的项目构建工具。它可以自动运行你所设定的任务。

**webpack**webpack是近期最火的一款模块加载器兼打包工具，它能把各种资源，例如JS（含JSX）、coffee、样式（含less/sass）、图片等都作为模块来使用和处理。

### 1.3 未来展望 {#13-未来展望}

随着JavaScript的发展，前端工作面对越来越多的问题，例如：性能优化、js/css文件的依赖问题，提升开发效率等越来越突出，这就需要使用自动化构建工具来替代我们做更多的工作。

gulp和grunt作为前端构建工具，gulp依赖于nodeJS stream，工作速度相对于grunt更快，配置文件更加简洁。受到越来越多前端工作者 的青睐。

Gulp 就是为了规范前端开发流程，实现前后端分离、模块化开发、版本控制、文件合并与压缩、mock数据等功能的一个前端自动化构建工具，而Webpack 是当下最热门的前端资源模块化管理和打包工具。它可以将许多松散的模块按照依赖和规则打包成符合生产环境部署的前端资源。还可以将按需加载的模块进行代码分隔，等到实际需要的时候再异步加载。

可以看出Gulp侧重于前端开发的 整个过程 的控制管理（像是流水线），我们可以通过给gulp配置不通的task（通过Gulp中的gulp.task\(\)方法配置，比如启动server、sass/less预编译、文件的合并压缩等等）来让gulp实现不同的功能，从而构建整个前端开发流程。

Webpack有人也称之为模块打包机，由此也可以看出Webpack更侧重于模块打包，当然我们可以把开发中的所有资源（图片、js文件、css文件等）都可以看成模块，最初Webpack本身就是为前端JS代码打包而设计的，后来被扩展到其他资源的打包处理。

两者各有侧重，前端工作中组合使用会更加方便。

另一方面，gulp的相关插件已经由2016年的1000多个，发展到了2900多个。说明了gulp生态圈已经相当稳定。或将取代grunt成为了前端的一大开发利器。

## 第二章 {#第二章}

### 2.1 gulp安装 {#21-gulp安装}

gulp是基于nodeJS，安装nodejs：下载nodeJS安装包，安装NodeJS；配置npm的全局路径：

* node安装

> 官网下载node安装包：[https://nodejs.org](https://nodejs.org/);
>
> windows:直接下一步下一步式安装。安装好后WIN+R输入cmd调出DOS窗口，输入node看是否有交互，如果没有则查看系统变量Path，把path配置上去
>
> node -v \#检测node安装成功

配置npm全局路径

> Windows下的Nodejs npm路径是appdata，可能不是我们想要的路径，可以改成我们指定的路径方便管理。 在cmd下执行以下命令 npm config set cache “D:\nodejs\node\_cache” npm config set prefix “D:\nodejs\node\_global” 如果命令无效，可以去nodejs的安装目录中找到node\_modules\npm\npmrc文件，这个文件存放npm的userconfig配置。 修改如下即可：
>
> prefix = D:\nodejs\node\_global
>
> cache = D:\nodejs\ node\_cache

* gulp安装

全局安装gulp：

> npm install gulp -g \#全局安装gulp npm install -D gulp \#作为项目依赖\(devDependencies\)安装
>
> gulp -v \#检查是否安装成功

* gulp使用

在项目根目录下创建一个名为gulpfile.js文件：

```
var gulp = require('gulp');
gulp.task('default', function(){
    //默认任务代码
})

```

## 第二章 gulp的安装使用 {#第二章-gulp的安装使用}

### 2.1 安装gulp命令行工具 {#21-安装gulp命令行工具}

* 全局安装gulp

```
npm install -g gulp  //全局环境下安装gulp
gulp -v              //gulp 是否安装成功；正确安装出现版本信息
npm install --save-dev gulp //将gulp加入到项目的开发依赖中

```

> **tips**: gulp是一个基于NodeJs的前端代码构建工具，安装gulp首先应当安装node；

* 安装gulp插件：

  gulp插件应当加入到项目依赖（devDependencies）中：

```
npm install --save-dev 
<
plugin name
>
         //--save-dev插件安装到项目依赖中

```

gulp插件查询地址：

* [http://gulpjs.com/plugins/](http://gulpjs.com/plugins/)
* [https://www.npmjs.com/browse/keyword/gulpplugin](https://www.npmjs.com/browse/keyword/gulpplugin)

### 2.2 gulp 使用 {#22-gulp-使用}

* 配置gulpfile.js文件

  在项目根目录下创建一个名为 gulpfile.js 的文件：

  ```
  var gulp = require('gulp');          //引入gulp

  gulp.task('default', function() {
    // 将默认的任务代码放在这里
  });

  ```

* 运行gulp

  ```
  $ gulp

  ```

  项目文件目录下，命令行输入gulp，会运行在gulpfile.js中定义的默认的任务；

  ```
  $ gulp 
  <
  task
  >
  ```

  运行 gulp + task\_name 会运行特定的 task\_name 的任务

* gulp API

**gulp.src\(globs\[, options\]\)：**

输出（Emits）符合所提供的匹配模式（glob）或者匹配模式的数组（array of globs）的文件。 将返回一个 Vinyl files 的 stream 它可以被 piped 到别的插件中。

**gulp.dest\(path\[, options\]\)**

能被 pipe 进来，并且将会写文件。并且重新输出（emits）所有数据，因此你可以将它 pipe 到多个文件夹。如果某文件夹不存在，将会自动创建它。

**gulp.task\(name\[, deps\], fn\)**

可以使用命令行gulp \[task\] 来完成task定义的任务；

deps为gulp\[taskName\]的依赖依赖； 当deps的代码运行完毕，即会执行gulp定义的相关任务；注意事项：gulp的依赖只会在代码执行完毕就马上 执行相关的任务，而不会等待依赖定义的相关的异步任务；如果想要解决相关问题，被依赖的task可以设置回调函数，当任务完成时返回一个stream或者异步的promise；

''' var gulp = require\('gulp'\); // var Q = require\('q'\); var num=1; gulp.task\('a', function\(\){ setTimeout\(function\(\){ console.log\("a: "+num\); num++; },1000\); }\);

gulp.task\('b',\['a'\],function\(\){ console.log\("b: "+num\); }\);

gulp.task\('default', \['a', 'b'\],function\(\){ console.log\("default: "+3\) }\); '''

**gulp.watch\(glob \[, opts\], tasks\) 或 gulp.watch\(glob \[, opts, cb\]\)**

监视文件，并且可以在文件发生改动时候做一些事情。它总会返回一个 EventEmitter 来发射（emit） change 事件。

**gulp.run\(tasks...\)**+

尽可能多的并行运行多个task;

