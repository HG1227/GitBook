# 初识React

#### 作者：高天阳
#### 邮箱：13683265113@163.com

```
更改历史

* 2019-08-16        高天阳     补充文档
* 2018-07-11        高天阳     初始化文档

```

## React简介

React是一个用于构建用户界面的JAVASCRIPT库，主要用于构建UI，它起源于**Facebook**的内部项目，用来架设Instagram的网站，并于**2013年5月开源**。
截止18年，React已经成为**使用人数最多**的前端框架，拥有着十分**健全的文档与完善的社区**。

React主要有三大类应用

* React JS 主要用于网页应用的构建
* React Native 主要用于原生应用的构建
* React VR 主要用于VR应用(全景视图应用)的构建

### React Fiber是什么

React16之后的版本统称，主要是对底层核心算法进行了优化，引入了优先级的概念、分片的概念，可以使代码运行的更加流畅，尤其是针对一些复杂的动画。

### React 特点

1. **高效** − React通过对DOM的模拟，最大限度地减少与DOM的交互。
2. **灵活** − React可以与已知的库或框架很好地配合。
3. **JSX** − JSX 是 JavaScript 语法的扩展。React 开发不一定使用 JSX ，但React建议使用它。
4. **组件** − 通过 React 构建组件，使得代码更加容易得到复用，能够很好的应用在大项目的开发中。
5. **单向响应的数据流** − React 实现了单向响应的数据流，从而减少了重复代码，这也是它为什么比传统数据绑定更简单。

## 快速构建 React 开发环境

安装较新版本的Node.js，并使用npx命令安装React App

[创建新的 React 应用](https://react.docschina.org/docs/create-a-new-react-app.html#create-react-app)

```
npx create-react-app my-app
cd my-app
npm start
```

> **注意**
>
> 第一行的 npx 不是拼写错误 —— 它是 npm 5.2+ 附带的 package 运行工具。

## JSX

JSX是JavaScript的语法扩展,利用JSX编写DOM结构，可以用原生的HTML标签，也可以直接像普通标签一样引用React组件。
这两者约定通过大小写来区分，小写的**字符串**是HTML标签，大写开头的**变量**是React组件。

实例：JSX中使用JavaScript表达式，表达式可写在花括号{}中：

```
ReactDOM.render(
    <div> 
        {1+1}
    </div> ,
    document.getElementById('example') 
);
```

## React 渲染元素

元素就是您要在屏幕上看到的内容，例如：

```
const element = <h1>Hello, world</h1>;
```

假设你的HTML文件有一个`<div>： <div id=“root”></div>`我们称之为“根”DOM节点，其中的所有内容都将由React DOM进行管理，
要将React元素渲染到根DOM节点中，请将其两者都传递给ReactDOM.render()：

```
const element = <h1>Hello, world</h1>;
ReactDOM.render(
    element,
    document.getElementById('root')
);
```

## React 组件

组件可以让您将UI拆分成独立的可重复使用的部分，组件就像JavaScript函数。他们接受任意输入，并返回应该在屏幕上显示的React元素。

```
class Welcome extends Component {
    render() {
        return (
            <h1>Hello world</h1>
        );
    }
}
```

使用定义的组件：

```
ReactDOM.render(< Welcome />, document.getElementById('root'));
```
