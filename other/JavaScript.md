# 前段面试题

#### 作者：高天阳
#### 邮箱：13683265113@163.com

```
更改历史

* 2018-11-28        高天阳     初始化文档

```

## 1 让下面的代码可以运行：

```javascript
const a = [1, 2, 3, 4, 5];
// Implement this
const multiply = function() {
  // do something
}
a.multiply();
console.log(a); // [1, 2, 3, 4, 5, 1, 4, 9, 16, 25]
```

答：

```javascript
const a = [1, 2, 3, 4, 5];
// Implement this
const multiply = function() {
  // do something
  // 如果不存储a.length，会导致a.length无限增长导致死循环
  var b = a.length
  for (var i = 0; i < b; i++) {
    a.push(a[i]*a[i])
  }
}
a.multiply();
console.log(a); // [1, 2, 3, 4, 5, 1, 4, 9, 16, 25]
```

## 2 以下代码会返回false，解释为什么会这样：

```javascript
// false
0.2 + 0.1 === 0.3
```

答：实际上是因为计算机内部的信息都是由二进制方式表示的，即0和1组成的各种编码，
但由于某些浮点数没办法用二进制准确的表示出来，也就带来了一系列精度问题。

```javascript
var accAdd = function(num1, num2) {
    num1 = Number(num1);
    num2 = Number(num2);
    var dec1, dec2, times;
    try { dec1 = countDecimals(num1)+1; } catch (e) { dec1 = 0; }
    try { dec2 = countDecimals(num2)+1; } catch (e) { dec2 = 0; }
    times = Math.pow(10, Math.max(dec1, dec2));
    // var result = (num1 * times + num2 * times) / times;
    var result = (accMul(num1, times) + accMul(num2, times)) / times;
    return getCorrectResult("add", num1, num2, result);
    // return result;
};
 
var accSub = function(num1, num2) {
    num1 = Number(num1);
    num2 = Number(num2);
    var dec1, dec2, times;
    try { dec1 = countDecimals(num1)+1; } catch (e) { dec1 = 0; }
    try { dec2 = countDecimals(num2)+1; } catch (e) { dec2 = 0; }
    times = Math.pow(10, Math.max(dec1, dec2));
    // var result = Number(((num1 * times - num2 * times) / times);
    var result = Number((accMul(num1, times) - accMul(num2, times)) / times);
    return getCorrectResult("sub", num1, num2, result);
    // return result;
};
 
var accDiv = function(num1, num2) {
    num1 = Number(num1);
    num2 = Number(num2);
    var t1 = 0, t2 = 0, dec1, dec2;
    try { t1 = countDecimals(num1); } catch (e) { }
    try { t2 = countDecimals(num2); } catch (e) { }
    dec1 = convertToInt(num1);
    dec2 = convertToInt(num2);
    var result = accMul((dec1 / dec2), Math.pow(10, t2 - t1));
    return getCorrectResult("div", num1, num2, result);
    // return result;
};
 
var accMul = function(num1, num2) {
    num1 = Number(num1);
    num2 = Number(num2);
    var times = 0, s1 = num1.toString(), s2 = num2.toString();
    try { times += countDecimals(s1); } catch (e) { }
    try { times += countDecimals(s2); } catch (e) { }
    var result = convertToInt(s1) * convertToInt(s2) / Math.pow(10, times);
    return getCorrectResult("mul", num1, num2, result);
    // return result;
};
 
var countDecimals = function(num) {
    var len = 0;
    try {
        num = Number(num);
        var str = num.toString().toUpperCase();
        if (str.split('E').length === 2) { // scientific notation
            var isDecimal = false;
            if (str.split('.').length === 2) {
                str = str.split('.')[1];
                if (parseInt(str.split('E')[0]) !== 0) {
                    isDecimal = true;
                }
            }
            let x = str.split('E');
            if (isDecimal) {
                len = x[0].length;
            }
            len -= parseInt(x[1]);
        } else if (str.split('.').length === 2) { // decimal
            if (parseInt(str.split('.')[1]) !== 0) {
                len = str.split('.')[1].length;
            }
        }
    } catch(e) {
        throw e;
    } finally {
        if (isNaN(len) || len < 0) {
            len = 0;
        }
        return len;
    }
};
 
var convertToInt = function(num) {
    num = Number(num);
    var newNum = num;
    var times = countDecimals(num);
    var temp_num = num.toString().toUpperCase();
    if (temp_num.split('E').length === 2) {
        newNum = Math.round(num * Math.pow(10, times));
    } else {
        newNum = Number(temp_num.replace(".", ""));
    }
    return newNum;
};
 
var getCorrectResult = function(type, num1, num2, result) {
    var temp_result = 0;
    switch (type) {
        case "add":
            temp_result = num1 + num2;
            break;
        case "sub":
            temp_result = num1 - num2;
            break;
        case "div":
            temp_result = num1 / num2;
            break;
        case "mul":
            temp_result = num1 * num2;
            break;
    }
    if (Math.abs(result - temp_result) > 1) {
        return temp_result;
    }
    return result;
}

// 加法： 
accAdd(0.1, 0.2)  // 得到结果：0.3
// 减法： 
accSub(1, 0.9)    // 得到结果：0.1
// 除法： 
accDiv(2.2, 100)  // 得到结果：0.022
// 乘法： 
accMul(7, 0.8)    // 得到结果：5.6
```

[如何避开JavaScript浮点数计算精度问题（如0.1+0.2!==0.3）](https://blog.csdn.net/u013347241/article/details/79210840)

## 3 JavaScript 中有哪些不同的数据类型？

> 提示：JavaScript 中只有两种类型——主要数据类型和引用类型（对象），其中有六种主要数据类型。

答：

* 基本数据类型
    * Number
    * String
    * Boolean
    * Null
    * Undefined
* 引用数据类型
    * Object
    * Array
    * Function
    * Data

[JavaScript中基本数据类型和引用数据类型的区别](https://www.cnblogs.com/cxying93/p/6106469.html)

## 4 解决以下异步代码问题。

获取并计算属于某个班级（假设 ID 为 75）的每个学生的平均分数。每个学生在一年内可以参加一门或多门课程。以下 API 可用于获取所需的数据。

```
// GET LIST OF ALL THE STUDENTS
GET /api/students
Response:
[{
    "id": 1,
    "name": "John",
    "classroomId": 75
}]
// GET COURSES FOR GIVEN A STUDENT
GET /api/courses?filter=studentId eq 1
Response:
[{
    "id": "history",
    "studentId": 1
}, {
    "id": "algebra",
    "studentId": 1
},]
// GET EVALUATION FOR EACH COURSE
GET /api/evaluation/history?filter=studentId eq 1
Response:
{
    "id": 200,
    "score": 50,
    "totalScore": 100
}
```

编写一个以班级 ID 作为参数的函数，你将使用这个函数计算该班级中每个学生的平均分数。这个函数的最终输出应该是带有平均分数的学生列表：

```json
[
    { "id": 1, "name": "John", "average": 70.5 },
    { "id": 3, "name": "Lois", "average": 67 }
]
```

使用普通回调、promises、observables、generator 或 async-wait 编写所需的函数。尝试使用至少 3 种不同的技术解决这个问题。

答：

## 5 使用 JavaScript 代理实现简单的数据绑定:
     
> 提示：ES Proxy 允许你拦截对任何对象属性或方法的调用。首先，每当底层绑定对象发生变更时，都应更新 DOM。

答：

## 6 解释 JavaScript 的并发模型:

你是否熟悉 Elixir、Clojure、Java 等其他编程语言中使用的并发模型？

> 提示：事件循环、任务队列、调用栈、堆等。

答：

## 7 “new”关键字在 JavaScript 中有什么作用？

> 提示：在 JavaScript 中，new 是用于实例化对象的运算符。
  
> 另外，请注意 `[[Construct]]` 和 `[[Call]]`。

答：

## 8 JavaScript 中有哪些不同的函数调用模式？请详细解释。
     
> 提示：有四种模式，函数调用、方法调用、.call() 和.apply()。

答：

## 9 介绍一些即将发布的新的 ECMAScript 提案。
     
> 提示：与 2018 年一样，BigInt、部分函数、管道操作符等。

答：

## 10 JavaScript 中的 iterator 和 iterable 是什么？你知道有哪些内置的 iterator 吗？

答：

## 11 为什么 JavaScript 类被认为是一种反模式？
      
JavaScript 的类是否还有其他用武之地？

答：

## 12 如何将下面的对象序列化成 JSON？
      
如果我们将下面的对象转换为 JSON 字符串，会发生什么？

```javascript
const a = {
 key1: Symbol(),
 key2: 10
}
// What will happen?
console.log(JSON.stringify(a));
```

答：

## 13 你熟悉 Typed Arrays 吗？如果是，请解释它们的用处以及它们与传统数组的差别？

答：

## 14 请解释默认参数的原理？
      
如果我们在调用 makeAPIRequest 函数时使用默认的 timeout，那么正确的语法是怎样的？

```javascript
function makeAPIRequest(url, timeout = 2000, headers) {
 // Some code to fetch data
} 
```

答：

## 15 解释什么是 TCO——尾部调用优化。有没有支持尾部调用优化的 JavaScript 引擎？
      
> 提示：截至 2018 年，没有。
      
答：

## 参考资料

* [这是今年前端最常见的面试题，你都会了吗？](https://www.toutiao.com/a6628352915134218765/?tt_from=weixin&utm_campaign=client_share&wxshare_count=1&timestamp=1543372749&app=news_article&utm_source=weixin&iid=51295460021&utm_medium=toutiao_ios&group_id=6628352915134218765)

