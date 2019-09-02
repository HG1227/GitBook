# react-router

#### 作者：高天阳
#### 邮箱：13683265113@163.com

```
更改历史

* 2019-09-02	    高天阳	初始化文档

```

## 前言

真正学会 [React](https://reactjs.org) 是一个漫长的过程。

你会发现，它不是一个库，也不是一个框架，而是一个庞大的体系。想要发挥它的威力，整个技术栈都要配合它改造。
你要学习一整套解决方案，从后端到前端，都是全新的做法。

举例来说，React 不使用 HTML，而使用 JSX 。它打算抛弃 DOM，要求开发者不要使用任何 DOM 方法。
它甚至还抛弃了 SQL ，自己发明了一套查询语言 GraphQL 。当然，这些你都可以不用，React 照样运行，但是就发挥不出它的最大威力。

这样说吧，你只要用了 React，就会发现合理的选择就是，采用它的整个技术栈。

本文介绍 React 体系的一个重要部分：路由库[React-Router](https://github.com/ReactTraining/react-router)。
它是官方维护的，事实上也是唯一可选的路由库。它通过管理 URL，实现组件的切换和状态的变化，开发复杂的应用几乎肯定会用到。

## 背景

react-router就是一个决定生成什么父子关系的组件，一般和layout结合起来，保证layout不行，内部的子html进行跳转

你会发现，它不是一个库，也不是一个框架，而是一个庞大的体系。想要发挥它的威力，整个技术栈都要配合它改造。
你要学习一整套解决方案，从后端到前端，都是全新的做法

## 快速开始

### 安装

```
npm install -S react-router-dom
```

### 使用

使用时，路由器Router就是React的一个组件。

```
import { Router } from 'react-router-dom';
render(<Router/>, document.getElementById('app'));
```

### 基本路由

在下面这个例子中，我们有3个'Page'组件处理<Router>。注意：我们使用`<Link to="/">`而不是`<a href="/">`。

```
import React from "react";
import { BrowserRouter as Router, Route, Link } from "react-router-dom";

function Index() {
  return <h2>Home</h2>;
}

function About() {
  return <h2>About</h2>;
}

function Users() {
  return <h2>Users</h2>;
}

function AppRouter() {
  return (
    <Router>
      <div>
        <nav>
          <ul>
            <li>
              <Link to="/">Home</Link>
            </li>
            <li>
              <Link to="/about/">About</Link>
            </li>
            <li>
              <Link to="/users/">Users</Link>
            </li>
          </ul>
        </nav>

        <Route path="/" exact component={Index} />
        <Route path="/about/" component={About} />
        <Route path="/users/" component={Users} />
      </div>
    </Router>
  );
}

export default AppRouter;
```

上面代码中，用户访问根路由`/`（比如`http://www.example.com/`），组件APP就会加载到`document.getElementById('app')`。

你可能还注意到，Router组件实际上是[BrowserRouter](./react-router-dom.md)组件起的别名，

它的值hashHistory表示，路由的切换由URL的hash变化决定，即URL的#部分发生变化。
举例来说，用户访问`http://www.example.com/`，实际会看到的是`http://www.example.com/#/`。

Route组件定义了URL路径与组件的对应关系。你可以同时使用多个Route组件。

```
<Router history={hashHistory}>
  <Route path="/" component={App}/>
  <Route path="/repos" component={Repos}/>
  <Route path="/about" component={About}/>
</Router>
```

上面代码中，用户访问`/repos`（比如`http://localhost:8080/#/repos`）时，加载Repos组件；
访问`/about`（`http://localhost:8080/#/about`）时，加载About组件。

### 嵌套路由

Route组件还可以嵌套。

```
<Router history={hashHistory}>
  <Route path="/" component={App}>
    <Route path="/repos" component={Repos}/>
    <Route path="/about" component={About}/>
  </Route>
</Router>
```

上面代码中，用户访问/repos时，会先加载App组件，然后在它的内部再加载Repos组件。

```
<App>
  <Repos/>
</App>
```

App组件要写成下面的样子。

```
export default React.createClass({
  render() {
    return <div>
      {this.props.children}
    </div>
  }
})
```

上面代码中，App组件的this.props.children属性就是子组件。

子路由也可以不写在Router组件里面，单独传入Router组件的routes属性。

```
let routes = <Route path="/" component={App}>
  <Route path="/repos" component={Repos}/>
  <Route path="/about" component={About}/>
</Route>;

<Router routes={routes} history={browserHistory}/>
```

### path 属性
### 通配符
### IndexRoute 组件
### Redirect 组件
### IndexRedirect 组件
### Link
### IndexLink
### histroy 属性
### 表单处理
### 路由的钩子

## API


## 示例

## 同类技术比较


## 参考资料

* [react-router官方文档](https://reacttraining.com/react-router/web/guides/quick-start)
* [React Router 使用教程](https://www.cnblogs.com/qiangxia/p/5646194.html)
* [react-router、react-redux、antd（Layout）](https://www.jianshu.com/p/54e21ddae130)
* [React-Router基础（<BrowserRouter>）](https://www.cnblogs.com/xingxingclassroom/p/10740148.html)


