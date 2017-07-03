### 课堂笔记

简介

Javascript单元测试工具

Jest是白盒测试

白盒测试:知道程序内部逻辑结构，进行测试

\(黑盒测试:不知道程序内部逻辑进行测试\)

\(灰盒测试:介于黑白之间的\)

单元格测试:针对函数测试

下载

Matchers

测试

Promise是一个异步对象vue中的axios就用到这个对象

.then\(\)成功执行

.catch\(\)失败执行

Vim:wq保存并退出:!q强制退出

# jest {#82-jest}

## 第一章 jest入门 {#第一章-jest入门}

### 1.1 jest简介 {#11-jest简介}

* Jest是Facebook开发的一个对javascript进行单元测试的工具，之前仅在其内部使用，后开源，并且是在Jasmine测试框架上演变开发而来，使用了我们熟知的expect\(value\).toBe\(other\)这种断言格式

* jest是白盒测试，即为知道程序内部逻辑结构。要求测试人员有一定的技术知识。

* jest是单元格测试，即对函数进行测试。每个函数视为一个单元。

### 1.2 jest下载与简单使用 {#12-jest下载与简单使用}

1, 安装Jest使用npm：

```
npm install --save-dev jest

```

  
2, 创建一个sum.js文件内容为：

```
const sum = require('./sum');

test('adds 1 + 2 to equal 3', () =
>
 {
  expect(sum(1, 2)).toBe(3);
});

```

3, 在sum相同的目录下创建sum.test.js文件\(为什么叫\_\_test\_\_?见官网首页\)

```
const sum = require('./sum');

test('adds 1 + 2 to equal 3', () =
>
 {
  expect(sum(1, 2)).toBe(3);
});

```

4, package.json添加以下部分:

```
{
  "scripts": {
    "test": "jest"
  }
}

```

5, 终端输入`npm test`,打印出测试结果：

```
PASS  ./sum.test.js
✓ adds 1 + 2 to equal 3 (5ms)

```

### 1.3 jest Matchers {#13-jest-matchers}

1, 什么是Matchers？

```
test('adds 1 + 2 to equal 3', () =
>
 {
  expect(sum(1, 2)).toBe(3);
});

```

上面代码块中的`expect`函数返回一个对像，Matchers就是这个对象的一些方法，比如`.toBe()`

2, Macther的作用？

Macther是用来比较值的，举个栗子:`expect(1234)`中的`1234`是实际值，Machter`toBe(2468)`中的`2468`便是期望值，Macher会比较这个值。栗子中我们是使用的是`toBe`（全等于），如果`1234`全等于`2468`则通过（pass）,否则fail.

3，常用的Macther

**toBe\(\)**

全等于，之所以叫全等于是因为它用的其实js中的`====`

```
test('object assignment', () =
>
 {
  const data = {one: 1};
  data['two'] = 2;
  expect(data).toEqual({one: 1, two: 2});
});

```

**toEqual\(\)**

用于测试`object`和`array`是否相等，它会遍历到没每一项进行比较

```
test('adding positive numbers is not zero', () =
>
 {
  for (let a = 1; a 
<
 10; a++) {
    for (let b = 1; b 
<
 10; b++) {
      expect(a + b).not.toBe(0);
    }
  }
});

```

**not**

取反

```
test('adding positive numbers is not zero', () =
>
 {
  for (let a = 1; a 
<
 10; a++) {
    for (let b = 1; b 
<
 10; b++) {
      expect(a + b).not.toBe(0);
    }
  }
});

```

### jest测试promise {#jest测试promise}

```
var getName = new  Promise（function（resolve，reject） {
    setTimeout（function（） {
        resolve（'jiangwei'）
    }）;
}）;

test('the data is jiangwei', () =
>
 {
  return getName().then(data =
>
 {
    expect(data).toBe('jiangwei');
  });
});
```



