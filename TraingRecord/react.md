# 初识React

## React简介

React 是一个用于构建用户界面的 JAVASCRIPT 库，主要用于构建UI，它起源于 Facebook 的内部项目，用来架设 Instagram 的网站，并于 2013 年 5 月开源。

#### React 特点

1. **高效** − React通过对DOM的模拟，最大限度地减少与DOM的交互。
2. **灵活** − React可以与已知的库或框架很好地配合。
3. **JSX** − JSX 是 JavaScript 语法的扩展。React 开发不一定使用 JSX ，但React建议使用它。
4. **组件** − 通过 React 构建组件，使得代码更加容易得到复用，能够很好的应用在大项目的开发中。
5. **单向响应的数据流** − React 实现了单向响应的数据流，从而减少了重复代码，这也是它为什么比传统数据绑定更简单。

## 快速构建 React 开发环境
```
npm install -g create-react-app
create-react-app [name]
```

## JSX
JSX是JavaScript的语法扩展,利用 JSX 编写 DOM 结构，可以用原生的 HTML 标签，也可以直接像普通标签一样引用 React 组件。
这两者约定通过大小写来区分，小写的**字符串**是 HTML 标签，大写开头的**变量**是 React 组件。

实例：JSX 中使用 JavaScript 表达式，表达式可写在花括号 {} 中：
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

假设你的HTML文件有一个<div>： <div id=“root”></div>我们称之为“根”DOM节点，其中的所有内容都将由React DOM进行管理，要将React元素渲染到根DOM节点中，请将其两者都传递给ReactDOM.render()：
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