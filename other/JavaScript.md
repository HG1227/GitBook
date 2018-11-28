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

## 2 以下代码会返回false，解释为什么会这样：

```javascript
// false
0.2 + 0.1 === 0.3
```

答：

## 3 JavaScript 中有哪些不同的数据类型？

> 提示：JavaScript 中只有两种类型——主要数据类型和引用类型（对象），其中有六种主要数据类型。

答：

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
