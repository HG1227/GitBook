# async/await

#### 作者：高天阳
#### 邮箱：13683265113@163.com

```
更改历史

* 2019-09-19        高天阳     初始化文档

```

## 简介

### 什么是async/await

async [ə'zɪŋk]：这个单词看起来很怪异，它的原型是asynchrony，意为异步。

可能有的人看了这个词想到了放在script标签里的异步脚本，但是此async非彼[async](https://www.jianshu.com/p/66db7d62d827)，
这个async是ES2017出来的，也是用来处理异步的，和ES6中的promise类似。

### async与Promise、generator有什么差别

nodeJs里面有一个典型的异步操作，下面用三种异步处理方式来读取文件readFile()：

#### promise来读取文件

```javascript
// promise.js
const fs = require("fs");
const read = function(fileName){
    return new Promise((resolve,reject)=>{
        fs.readFile(fileName,(err,data)=>{
            if (err) {
                reject(err);
            } else{
                resolve(data);
            }
        });
    });
};
read('1.txt').then(res=>{
    console.log(res.toString());
    return read('2.txt');  // 返回新的数据，然后输出
}).then(res => {
    console.log(res.toString());
    return read('3.txt');
}).then(res => {
    console.log(res.toString());
});
```

然后用node来运行该文件，打开命令行(win+r)：

![](../assets/Es6/async1.png)

因为读取多个文件一般都会作为一个异步来处理，这样就不会阻塞程序的运行，
把fs封装成一个Promise对象，然后在下面返回数据输出，例子中的TXT文件可以写自己的数据

#### generator函数读取文件

```javascript
// generator.js
const fs = require("fs");
const read = function(fileName){
    return new Promise((resolve,reject)=>{
        fs.readFile(fileName,(err,data)=>{
            if (err) {
                reject(err);
            } else{
                resolve(data);
            }
        });
    });
};
function * show(){
    yield read('1.txt');
    yield read('2.txt');
    yield read('3.txt');
}
const s = show();
s.next().value.then(res => {
    console.log(res.toString());
    return s.next().value;
}).then(res => {
    console.log(res.toString());
    return s.next().value;
}).then(res => {
    console.log(res.toString());
});
```

依然用node运行即可，这种方式代码量又高了不少，和Promise方式特别像，
只不过是把读取文件的信息放在了外面，在下面依次手动调用，特别麻烦.

#### async函数读取文件

```javascript
const fs = require("fs");
const read = function(fileName){
    return new Promise((resolve,reject)=>{
        fs.readFile(fileName,(err,data)=>{
            if (err) {
                reject(err);
            } else{
                resolve(data);
            }
        });
    });
};
async function readByAsync(){
    let a1 = await read('1.txt');
    let a2 = await read('2.txt');
    let a3 = await read('3.txt');
    console.log(a1.toString());
    console.log(a2.toString());
    console.log(a3.toString());
}
readByAsync();
```

这个函数和generator函数有些类似，从例子中可以看得出来，async函数在function前面有个async作为标识，
意思就是异步函数，里面有个await搭配使用，每到await的地方就是程序需要等待执行后面的程序，语义化很强.

## 特点

* 语义化强
* 里面的await只能在async函数中使用
* await后面的语句可以是Promise对象、数字、字符串等
* async函数返回的是一个Promise对象
* await语句后的Promise对象变成reject状态时，那么整个async函数会中断，后面的程序不会继续执行

基于上面的async的特点，我们会用到异常捕获机制，学过java的都知道，java中有异常捕获`try...catch...`

什么是`try...catch...`，下面让我们来看一下它的概念。

> try/catch/finally 语句用于处理代码中可能出现的错误信息。
  错误可能是语法错误，通常是程序员造成的编码错误或错别字。
  也可能是拼写错误或语言中缺少的功能（可能由于浏览器差异）。
  **try**语句允许我们定义在执行时进行错误测试的代码块。
  **catch** 语句允许我们定义当 **try** 代码块发生错误时，所执行的代码块。
  **finally** 语句在 try 和 catch 之后无论有无异常都会执行。<br>
  **注意**： catch 和 finally 语句都是可选的，但你在使用 try 语句时必须至少使用一个。<br>
  **提示**： 当错误发生时， JavaScript 会停止执行，并生成一个错误信息。
  使用 [throw](https://www.runoob.com/jsref/jsref-throw.html) 
  语句来创建自定义消息(抛出异常)。如果你将 **throw** 和 **try** 、**catch**一起使用，
  就可以控制程序输出的错误信息。

知道了这个东西是干什么的，那么我们在async中怎么用呢？

```javascript
const fs = require("fs");
const read = function(fileName){
    return new Promise((resolve,reject)=>{
        fs.readFile(fileName,(err,data)=>{
            if (err) {
                reject(err);
            } else{
                resolve(data);
            }
        });
    });
};
async function readByAsync(){
    try{
        let a1 = await read('1.txt');
        let a2 = await read('2.txt');
        let a3 = await read('3.txt');
    }catch(e){
        //TODO handle the exception
    }
    console.log(a1);
    console.log(a2);
    console.log(a3);
}
readByAsync();
```

大家看完了这个async是不是感觉还挺有用的啊，以后工作中async就会替代generator，原理是Promise，所以说特别好用。

## 示例

### async的基础用法

async作为一个关键字放到函数前面，用于表示函数是一个异步函数，因为async就是异步的意思，
异步函数也就意味着该函数的执行不会阻塞后面代码的执行。写一个async函数

```javascript
async function timeout() {
　　return 'hello world';
}
```

### async的调用

语法很简单，就是在函数前面加上async关键字，来表示它是异步的，那怎么调用呢？
async函数也是函数，平时我们怎么使用函数就怎么使用它，
直接加括号调用就可以了，为了表示它没有阻塞它后面代码的执行，我们在async 函数调用之后加一句`console.log`;

```javascript
async function timeout() {
    return 'hello world'
}
timeout();
console.log('虽然在后面，但是我先执行');
```

打开浏览器控制台，我们看到了

![](../assets/Es6/async2.png)

async函数timeout调用了，但是没有任何输出，它不是应该返回'hello world',先不要着急，
看一看timeout()执行返回了什么？把上面的timeout()语句改为console.log(timeout())

```javascript
async function timeout() {
    return 'hello world'
}
console.log(timeout());
console.log('虽然在后面，但是我先执行');
```

继续看控制台

![](../assets/Es6/async3.png)

原来async函数返回的是一个promise对象，如果要获取到promise返回值，我们应该用then方法，继续修改代码

```javascript
async function timeout() {
    return 'hello world'
}
timeout().then(result => {
    console.log(result);
})
console.log('虽然在后面，但是我先执行');
```

看控制台

![](../assets/Es6/async4.png)

我们获取到了"hello world', 同时timeout的执行也没有阻塞后面代码的执行，和我们刚才说的一致。

### async的回调

这时，你可能注意到控制台中的Promise有一个resolved，这是async函数内部的实现原理。
如果async函数中有返回一个值,当调用该函数时，
内部会调用Promise.solve()方法把它转化成一个promise对象作为返回，
但如果timeout函数内部抛出错误呢？那么就会调用Promise.reject()返回一个promise对象，
这时修改一下timeout函数

```javascript
async function timeout(flag) {
    if (flag) {
        return 'hello world'
    } else {
        throw 'my god, failure'
    }
}
console.log(timeout(true))  // 调用Promise.resolve() 返回promise 对象。
console.log(timeout(false)); // 调用Promise.reject() 返回promise 对象。
```

控制台如下：

![](../assets/Es6/async5.png)

如果函数内部抛出错误， promise 对象有一个catch 方法进行捕获。

```javascript
timeout(false).catch(err => {
    console.log(err)
})
```

### await的使用

async关键字差不多了，我们再来考虑await关键字，await是等待的意思，
那么它等待什么呢，它后面跟着什么呢？其实它后面可以放任何表达式，
不过我们更多的是放一个返回promise 对象的表达式。注意await关键字只能放到async函数里面

现在写一个函数，让它返回promise对象，该函数的作用是2s之后让数值乘以2

```javascript
// 2s 之后返回双倍的值
function doubleAfter2seconds(num) {
    return new Promise((resolve, reject) => {
        setTimeout(() => {
            resolve(2 * num)
        }, 2000);
    } )
}
```

现在再写一个async函数，从而可以使用await关键字， await后面放置的就是返回promise对象的一个表达式，
所以它后面可以写上doubleAfter2seconds函数的调用

```javascript
async function testResult() {
    let result = await doubleAfter2seconds(30);
    console.log(result);
}
```

现在调用testResult 函数

```javascript
testResult();
```

打开控制台，2s 之后，输出了60. 

现在我们看看代码的执行过程，调用testResult函数，它里面遇到了await, 
await表示等一下，代码就暂停到这里，不再向下执行了，它等什么呢？
等后面的promise对象执行完毕，然后拿到promise resolve的值并进行返回，
返回值拿到之后，它继续向下执行。具体到 我们的代码, 遇到await之后，
代码就暂停执行了，等待doubleAfter2seconds(30) 执行完毕，
doubleAfter2seconds(30) 返回的promise 开始执行，2秒之后，
promise resolve了，并返回了值为60， 这时await 才拿到返回值60，
然后赋值给result，暂停结束，代码才开始继续执行，执行console.log语句。

就这一个函数，我们可能看不出async/await的作用，如果我们要计算3个数的值，然后把得到的值进行输出呢？

```javascript
async function testResult() {
    let first = await doubleAfter2seconds(30);
    let second = await doubleAfter2seconds(50);
    let third = await doubleAfter2seconds(30);
    console.log(first + second + third);
}
```

6秒后，控制台输出220, 我们可以看到，写异步代码就像写同步代码一样了，再也没有回调地域了。

## 最佳实践

再写一个真实的例子，我原来做过一个小功能，话费充值，当用户输入电话号码后，
先查找这个电话号码所在的省和市，然后再根据省和市，找到可能充值的面值，进行展示。

为了模拟一下后端接口，我们新建一个node 项目。 新建一个文件夹 async, 
然后npm init -y 新建package.json文件，npm install express --save 安装后端依赖，
再新建server.js 文件作为服务端代码， public文件夹作为静态文件的放置位置，
在public 文件夹里面放index.html 文件， 整个目录如下











## 参考资料

* [深入浅出ES6教程『async函数』](https://www.jianshu.com/p/631f9406c4e0)
* [用 async/await 来处理异步](https://www.cnblogs.com/SamWeb/p/8417940.html)
* [ES6 Async/Await与Promise区别](https://www.cnblogs.com/JeneryYang/p/10113682.html)
