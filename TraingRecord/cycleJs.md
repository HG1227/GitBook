# cycle.js {#cyclejs}

## 第一章 定义 {#第一章-定义}

Cycle.js 是一个极简的JavaScript框架（核心部分加上注释125行），提供了一种函数式，响应式的人机交互接口

### 1.1 特性 {#11-特性}

* 函数式
 
  cycleJS将应用抽象成一个纯函数
  `main()`
  , 从外部世界读取副作用，然后产生输出（sinks）传递到外部世界，在那形成副作用。这些外部的副作用作为cycle的插件存在（drivers），他们负责处理DOM,处理HTTP请求等；
  ![](https://hxgqh.gitbooks.io/haomotraining/content/assets/qmyQ7bA.png)

> 在计算机编程中，假如满足下面这两个句子的约束，一个函数可能被描述为一个纯函数： 给出同样的参数值，该函数总是求出同样的结果。该函数结果值不依赖任何隐藏信息或程序执行处理可能改变的状态或在程序的两个不同的执行，也不能依赖来自I/O装置的任何外部的输入（通常是这样的--看下面的描述） 结果的求值不会促使任何可语义上可观察的副作用或输出，例如易变对象的变化或输出到I/O装置。

* 响应式  
  Cycle.js 使用 rx.js 来实现关注分离，这意味着应用程序是基于事件流的，数据流是 Observable 的；![](https://hxgqh.gitbooks.io/haomotraining/content/assets/VzuqqqI.png)

* HCI  
  HCI 是双向的对话，人机互为观察者：![](https://hxgqh.gitbooks.io/haomotraining/content/assets/jyMfYfQ.png)

* Drivers  
  driver 是 Cycle.js 主函数 main\(\) 和外部世界打交道的接口

* DOM Driver  
  即 @cycle/dom，是使用最为频繁的driver。实际应用中，我们的 main\(\) 会与DOM进行交互![](https://hxgqh.gitbooks.io/haomotraining/content/assets/FbY36ba.png)

* 组件化
 
  每个Cycle.js应用程序不管多复杂，都遵循一套输入输出的基本法，因此，组件化是很容易实现，无非就是函数对函数的组合调用

## 第二章 相似框架 {#第二章-相似框架}

* react
* vue

## 第三章 使用和说明 {#第三章-使用和说明}

这里的实战我们使用cycleJS官方提供的create-cycle-app来构建我们的项目；

### 3.1 项目初始化： {#31-项目初始化：}

使用npm安装create-cycle-app：

![](https://hxgqh.gitbooks.io/haomotraining/content/assets/downcreatecycleapp.png)

安装成功构建我们的app：

![](https://hxgqh.gitbooks.io/haomotraining/content/assets/createApp.png)![](https://hxgqh.gitbooks.io/haomotraining/content/assets/createSuc.png)

运行我们的App:

![](https://hxgqh.gitbooks.io/haomotraining/content/assets/runApp.png)![](https://hxgqh.gitbooks.io/haomotraining/content/assets/observal.png)

这样我们就能够在浏览器看到我们的第一个cycleJs的程序内容了

在程序中

Cycle.run是应用程序的入口，加载 main\(\) 和DOM driver，后者对一个HTML容器进行渲染输出

### 3.2 构建一个自己的简单的程序 {#32-构建一个自己的简单的程序}

在3.1的基础上我们使用`DOMDriver`,`HTTPDriver`来生成我们的样例：

* index.js

```
import {run} from '@cycle/run'  //
import {makeDOMDriver} from '@cycle/dom'
import {makeHTTPDriver} from '@cycle/http' //HTTPDriver
import {App} from './app'

const main = App

const drivers = {
  DOM: makeDOMDriver('#app'),
  HTTP: makeHTTPDriver()
}

run(main, drivers)

```

* app.js

```
import {div, button, h1, h4, a} from '@cycle/dom'; //DOMDrivers

export function App(sources) {
  const getRandomUser$ = sources.DOM.select('.get-random').events('click')
    .map(() =
>
 {
      const randomNum = Math.round(Math.random() * 9) + 1;
      return {
        url: 'https://jsonplaceholder.typicode.com/users/' + String(randomNum),
        category: 'users',
        method: 'GET'
      };
    });

  const user$ = sources.HTTP.select('users')
    .flatten()
    .map(res =
>
 res.body)
    .startWith(null);

  const vdom$ = user$.map(user =
>

    div('.users', [
      button('.get-random', 'Get random user'),
      user === null ? null : div('.user-details', [
        h1('.user-name', user.name),
        h4('.user-email', user.email),
        a('.user-website', {attrs: {href: user.website}}, user.website)
      ])
    ])
  );

  return {
    DOM: vdom$,
    HTTP: getRandomUser$
  };
}

```

我们运行npm start 就可以看到相关的页面，点击按钮出现搜索的任务信息![](https://hxgqh.gitbooks.io/haomotraining/content/assets/searchCy.png)

web应用程序通常需要从服务器获取和呈现数据；

假设我们有一个包含十个用户的数据库的后端。我们想拥有一个前端，一个按钮“获取随机用户”， 并显示用户的详细信息，如名称和电子邮件。

当我们点击按钮的时候，我们只需要向`/user/:number`接口发出请求，在cyclejs中，一般我们将http请求放在`HTTPDriver`中；

skins 是 main程序执行副作用的程序；并且来源是可读的副作用；在http请求相应中，HTTP请求是接收器，HTTP响应是源。

cycleJS中的 HTTP Driver也是一种类似于DOM风格的驱动程序；他需要一个sink stream（用于请求），并为我们提供源\(响应\),

如果当我们点击button时发送http请求，那么http请求将依赖于按钮点击事件流；getRandomUser$是我们向HTTP驱动程序提供的请求流，通过将其作为main\(\)函数中的接收器返回。

```
function main(sources) {
  // ...
  const click$ = sources.DOM.select('.get-random').events('click');

  const getRandomUser$ = click$.map(() =
>
 {
    const randomNum = Math.round(Math.random() * 9) + 1;
    return {
      url: 'https://jsonplaceholder.typicode.com/users/' + String(randomNum),
      category: 'users',
      method: 'GET'
    };
  });

  // ...

  return {
    // ...
    HTTP: getRandomUser$,
  };
}

```

我们仍然需要显示当前用户的数据，只有当我们收到HTTP响应时才会显示。为此，我们需要用户数据流直接依赖于HTTP响应流。这可以从main输入中获得：（sources.HTTP名称HTTP需要与您在调用时为HTTP驱动程序提供的驱动程序名称相匹配run\(\)）。

```
function main(sources) {
  // ...

  const user$ = sources.HTTP.select('users')
    .flatten()
    .map(res =
>
 res.body);

  // ...
}

```

sources.HTTP是一个“HTTP源”，代表此应用程序的所有网络响应。select\(category\)是特定于HTTP源的API，返回与category给定相关的所有响应流的流。因为该输出是流的流，所以我们应用flatten\(\)，以获得一个扁平化的响应流。检查上面的声明getRandomUser$，我们用一个category: users字段返回一个请求对象的位置。 如果希望深入了解这个原理请移步[HTTP驱动程序文档](https://github.com/cyclejs/cyclejs/tree/master/http);我们将每个响应映射res到res.body从响应中获取JSON数据，并忽略其他字段，如HTTP状态。

接下来，我们指定应用程序的呈现界面：在DOM中显示任何来自当前用户的信息user$；我们看到vdom$直接依赖user$；

最初，不会有任何user$事件，因为只有当用户点击时才会发生这种情况。

```
function main(sources) {
  // ...
  const vdom$ = user$.map(user =
>

    div('.users', [
      button('.get-random', 'Get random user'),
      div('.user-details', [
        h1('.user-name', user.name),
        h4('.user-email', user.email),
        a('.user-website', {href: user.website}, user.website)
      ])
    ])
  );
  // ...
}

```

这是我们在之前的“复选框”示例中看到的相同的“对话倡议”问题。所以我们需要user$从一个null用户开始，如果vdom$看到一个空的用户，它只会显示该按钮。否则，如果我们有真正的用户数据，我们还会显示他们的姓名，电子邮件和网站。

```
function main(sources) {
   // ...

   const user$ = sources.HTTP.select('users')
     .flatten()
     .map(res =
>
 res.body)
+    .startWith(null);

   const vdom$ = user$.map(user =
>

     div('.users', [
       button('.get-random', 'Get random user'),
-      div('.user-details', [
+      user === null ? null : div('.user-details', [
         h1('.user-name', user.name),
         h4('.user-email', user.email),
         a('.user-website', {href: user.website}, user.website)
       ])
     ])
   );

   // ...
 }

```

最终我们的代码就像上面实例看到的一样；呈现给我们简单的界面

而对于cyclejs而言，这些东西是远远不够的，这里只是为大家提供一个简单的入门，更多的信息例如：MVI设计模式，Driver编写等我们并没有涉及到，这些信息我们可以在参考文档中学习

## 第四章 参考文档 {#第四章-参考文档}

* [cyclejs官方文档](https://cycle.js.org/getting-started.html)
* [MVI设计模式](https://cycle.js.org/model-view-intent.html)
* [reactiveX.io](http://reactivex.io/)
* [Rx文档](http://xgrommx.github.io/rx-book/)



