# Qs

#### 作者：高天阳
#### 邮箱：13683265113@163.com

```
更改历史

* 2018-09-12	    高天阳	初始化文档

```

## 1 简介

qs 是一个增加了一些安全性的查询字符串解析和序列化字符串的库。

主要维护者：[Jordan Harband](https://github.com/ljharb)

在QS模块最初创建和维护[TJ Holowaychuk](https://github.com/tj/node-querystring)。

## 2 安装与使用

### 2.1 安装

#### 2.1.1 npm

qs是一个npm仓库所管理的包,可通过npm命令进行安装. 

```
npm install qs
```

#### 2.1.2 script引入

qs是一个npm仓库所管理的包,可通过npm命令进行安装. 

```
<script src="https://cdn.bootcss.com/qs/6.5.1/qs.min.js"></script>
```

[qs不同版本bootcdn链接](https://www.bootcdn.cn/qs/)

### 2.2 使用

```
var qs = require('qs');
var assert = require('assert');
 
var obj = qs.parse('a=c');
assert.deepEqual(obj, { a: 'c' });
 
var str = qs.stringify(obj);
assert.equal(str, 'a=c');
```

#### 2.2.1 解析对象

```
qs.parse(string, [options]);
```

qs允许您通过用方括号括起子键的名称来在查询字符串中创建嵌套对象[]。例如，字符串`foo[bar]=baz`转换为：

```
assert.deepEqual(qs.parse('foo[bar]=baz'), {
    foo: {
        bar: 'baz'
    }
});
```

使用该`plainObjects`选项时，解析后的值将作为空对象返回，通过`Object.create(null)`这样创建，
因此您应该知道原型方法不会存在，并且用户可以将这些名称设置为他们喜欢的任何值：

```
var nullObject = qs.parse('a[hasOwnProperty]=b', { plainObjects: true });
assert.deepEqual(nullObject, { a: { hasOwnProperty: 'b' } });
```

默认情况下，如果您希望保持这些字段中的数据`plainObjects`如上所述使用，或者设置`allowPrototypes`为`true`允许用户输入覆盖这些属性，
则会忽略将覆盖对象原型上的属性的参数。警告启用此选项通常是一个坏主意，因为在尝试使用已覆盖的属性时可能会导致问题。请务必小心此选项。

```
var protoObject = qs.parse('a[hasOwnProperty]=b', { allowPrototypes: true });
assert.deepEqual(protoObject, { a: { hasOwnProperty: 'b' } });
```

URI编码的字符串也有效：

```
assert.deepEqual(qs.parse('a%5Bb%5D=c'), {
    a: { b: 'c' }
});
```

您还可以嵌套对象，例如`foo[bar][baz]=foobarbaz`：

```
assert.deepEqual(qs.parse('foo[bar][baz]=foobarbaz'), {
    foo: {
        bar: {
            baz: 'foobarbaz'
        }
    }
});
```

默认情况下，嵌套对象时，qs最多只能解析5个子项。这意味着如果您尝试解析一个字符串，
就像`a[b][c][d][e][f][g][h][i]=j`您生成的对象一样 ：

```
var expected = {
    a: {
        b: {
            c: {
                d: {
                    e: {
                        f: {
                            '[g][h][i]': 'j'
                        }
                    }
                }
            }
        }
    }
};
var string = 'a[b][c][d][e][f][g][h][i]=j';
assert.deepEqual(qs.parse(string), expected);
```

通过将depth选项传递给以下可以覆盖此深度`qs.parse(string, [options])`：

```
var deep = qs.parse('a[b][c][d][e][f][g][h][i]=j', { depth: 1 });
assert.deepEqual(deep, { a: { b: { '[c][d][e][f][g][h][i]': 'j' } } });
```

当qs用于解析用户输入时，深度限制有助于减轻滥用，建议将其保持在相当小的数量。

出于类似的原因，默认情况下，qs最多只能解析1000个参数。这可以通过传递一个`parameterLimit`选项来覆盖：

```
var limited = qs.parse('a=b&c=d', { parameterLimit: 1 });
assert.deepEqual(limited, { a: 'b' });
```

要绕过前导问号，请使用`ignoreQueryPrefix`：

```
var prefixed = qs.parse('?a=b&c=d', { ignoreQueryPrefix: true });
assert.deepEqual(prefixed, { a: 'b', c: 'd' });
```

还可以传递可选的分隔符：

```
var delimited = qs.parse('a=b;c=d', { delimiter: ';' });
assert.deepEqual(delimited, { a: 'b', c: 'd' });
```

分隔符也可以是正则表达式：

```
var regexed = qs.parse('a=b;c=d,e=f', { delimiter: /[;,]/ });
assert.deepEqual(regexed, { a: 'b', c: 'd', e: 'f' });
```

选项`allowDots`可用于启用点表示法：

```
var withDots = qs.parse('a.b=c', { allowDots: true });
assert.deepEqual(withDots, { a: { b: 'c' } });
```

#### 2.2.2 解析数组

qs也可以使用类似的[]表示法解析数组：

```
var withArray = qs.parse('a[]=b&a[]=c');
assert.deepEqual(withArray, { a: ['b', 'c'] });
```

您也可以指定一个索引：

```
var withIndexes = qs.parse('a[1]=c&a[0]=b');
assert.deepEqual(withIndexes, { a: ['b', 'c'] });
```

请注意，数组中的索引与对象中的键之间的唯一区别是括号之间的值必须是一个数字才能创建数组。
在创建具有特定索引的数组时，qs会将稀疏数组压缩为仅保留其顺序的现有值：

```
var noSparse = qs.parse('a[1]=b&a[15]=c');
assert.deepEqual(noSparse, { a: ['b', 'c'] });
```

请注意，空字符串也是一个值，并将保留：

```
var withEmptyString = qs.parse('a[]=&a[]=b');
assert.deepEqual(withEmptyString, { a: ['', 'b'] });
 
var withIndexedEmptyString = qs.parse('a[0]=b&a[1]=&a[2]=c');
assert.deepEqual(withIndexedEmptyString, { a: ['b', '', 'c'] });
```

qs还会将数组中的索引指定为最大索引`20`。索引大于的任何数组成员`20`都将转换为以索引为键的对象：

```
var withMaxIndex = qs.parse('a[100]=b');
assert.deepEqual(withMaxIndex, { a: { '100': 'b' } });
```

通过传递`arrayLimit`选项可以覆盖此限制：

```
var withArrayLimit = qs.parse('a[1]=b', { arrayLimit: 0 });
assert.deepEqual(withArrayLimit, { a: { '1': 'b' } });
```

要完全禁用数组解析，请设置`parseArrays`为`false`。

```
var noParsingArrays = qs.parse('a[]=b', { parseArrays: false });
assert.deepEqual(noParsingArrays, { a: { '0': 'b' } });
```

如果混合符号，qs会将两个项合并为一个对象：

```
var mixedNotation = qs.parse('a[0]=b&a[b]=c');
assert.deepEqual(mixedNotation, { a: { '0': 'b', b: 'c' } });
```

您还可以创建对象数组：

```
var arraysOfObjects = qs.parse('a[][b]=c');
assert.deepEqual(arraysOfObjects, { a: [{ b: 'c' }] });
```

#### 2.2.3 字符串化

```
qs.stringify(object, [options]);
```

字符串化时，默认情况下，qs编码输出。对象按照您的预期进行字符串化：

```
assert.equal(qs.stringify({ a: 'b' }), 'a=b');
assert.equal(qs.stringify({ a: { b: 'c' } }), 'a%5Bb%5D=c');
```

可以通过将`encode`选项设置为以下来禁用此编码`false`：

```
var unencoded = qs.stringify({ a: { b: 'c' } }, { encode: false });
assert.equal(unencoded, 'a[b]=c');
```

通过将`encodeValuesOnly`选项设置为`true`：可以禁用键的编码：

```
var encodedValues = qs.stringify(
    { a: 'b', c: ['d', 'e=f'], f: [['g'], ['h']] },
    { encodeValuesOnly: true }
);
assert.equal(encodedValues,'a=b&c[0]=d&c[1]=e%3Df&f[0][0]=g&f[1][0]=h');
```

此编码也可以由设置为`encoder`选项的自定义编码方法替换：

```
var encoded = qs.stringify({ a: { b: 'c' } }, { encoder: function (str) {
    // 传递的值为'a`, `b`, `c`
    return // 返回已解码的字符串
}})
```

(注意：encoder如果encode是，该选项不适用false)

类似于encoder有一个decoder选项parse可以覆盖属性和值的解码：

```
var decoded = qs.parse('x=z', { decoder: function (str) {
    // 传递的值为'x`，`z`
    return // 返回已解码的字符串
}})
```

超出这一点的示例将显示为输出不是为了清晰起码而编码的URI。请注意，这些情况下的返回值将在实际使用期间进行URI编码。

当数组被字符串化时，默认情况下它们被赋予显式索引：

```
qs.stringify({ a: ['b', 'c', 'd'] });
// 'a[0]=b&a[1]=c&a[2]=d'
```

您可以通过将`indices`选项设置为以下来覆盖此选项`false`：

```
qs.stringify({ a: ['b', 'c', 'd'] }, { indices: false });
// 'a=b&a=c&a=d'
```

您可以使用该`arrayFormat`选项指定输出数组的格式：

```
qs.stringify({ a: ['b', 'c'] }, { arrayFormat: 'indices' })
// 'a[0]=b&a[1]=c'
qs.stringify({ a: ['b', 'c'] }, { arrayFormat: 'brackets' })
// 'a[]=b&a[]=c'
qs.stringify({ a: ['b', 'c'] }, { arrayFormat: 'repeat' })
// 'a=b&a=c'
```

对象进行字符串化时，默认情况下使用括号表示法：

```
qs.stringify({ a: { b: { c: 'd', e: 'f' } } });
// 'a[b][c]=d&a[b][e]=f'
```

您可以通过将`allowDots`选项设置为以下来覆盖此选项以使用点表示法`true`：

```
qs.stringify({ a: { b: { c: 'd', e: 'f' } } }, { allowDots: true });
// 'a.b.c=d&a.b.e=f'
```

空字符串和空值将省略该值，但等号（=）保持不变：

```
assert.equal(qs.stringify({ a: '' }), 'a=');
```

没有值的键（例如空对象或数组）将不返回任何内容：

```
assert.equal(qs.stringify({ a: [] }), '');
assert.equal(qs.stringify({ a: {} }), '');
assert.equal(qs.stringify({ a: [{}] }), '');
assert.equal(qs.stringify({ a: { b: []} }), '');
assert.equal(qs.stringify({ a: { b: {}} }), '');
```

设置为的属性`undefined`将完全省略：

```
assert.equal(qs.stringify({ a: null, b: undefined }), 'a=');
```

可以选择在查询字符串前面添加问号：

```
assert.equal(qs.stringify({ a: 'b', c: 'd' }, { addQueryPrefix: true }), '?a=b&c=d');
```

分隔符也可以用`stringify`覆盖：

```
assert.equal(qs.stringify({ a: 'b', c: 'd' }, { delimiter: ';' }), 'a=b;c=d');
```

如果您只想覆盖`Date`对象的序列化，则可以提供以下`serializeDate`选项：

```
var date = new Date(7);
assert.equal(qs.stringify({ a: date }), 'a=1970-01-01T00:00:00.007Z'.replace(/:/g, '%3A'));
assert.equal(
    qs.stringify({ a: date }, { serializeDate: function (d) { return d.getTime(); } }),
    'a=7'
);
```

您可以使用该`sort`选项来影响参数键的顺序：

```
function alphabeticalSort(a, b) {
    return a.localeCompare(b);
}
assert.equal(qs.stringify({ a: 'c', z: 'y', b : 'f' }, { sort: alphabeticalSort }), 'a=c&b=f&z=y');
```

最后，您可以使用该`filter`选项来限制字符串化输出中包含哪些键。
如果传递函数，将为每个键调用它以获取替换值。否则，如果传递数组，它将用于选择字符串化的属性和数组索引：

```
function filterFunc(prefix, value) {
    if (prefix == 'b') {
        // 返回`undefined`值以省略属性。
        return;
    }
    if (prefix == 'e[f]') {
        return value.getTime();
    }
    if (prefix == 'e[g][0]') {
        return value * 2;
    }
    return value;
}
qs.stringify({ a: 'b', c: 'd', e: { f: new Date(123), g: [2] } }, { filter: filterFunc });
// 'a=b&c=d&e[f]=123&e[g][0]=4'
qs.stringify({ a: 'b', c: 'd', e: 'f' }, { filter: ['a', 'e'] });
// 'a=b&e=f'
qs.stringify({ a: ['b', 'c', 'd'], e: 'f' }, { filter: ['a', 0, 2] });
// 'a[0]=b&a[2]=d'
```

### 2.3 示例

#### 2.3.1 qs.parse()

将URL解析成对象的形式

```
const Qs = require('qs');
let url = 'method=query_sql_dataset_data&projectId=85&appToken=7d22e38e-5717-11e7-907b-a6006ad3dba0';
Qs.parse(url);
console.log(Qs.parse(url));
```

如上面代码所示,输出结果如下: 

```
{
    method: 'query_sql_dataset_data',
    projectId: '85',
    appToken: '7d22e38e-5717-11e7-907b-a6006ad3dba0'
}
```

#### 2.3.2 qs.stringify()

将对象 序列化成URL的形式，以&进行拼接

```
const Qs = require('qs');
let obj= {
     method: "query_sql_dataset_data",
     projectId: "85",
     appToken: "7d22e38e-5717-11e7-907b-a6006ad3dba0",
     datasetId: " 12564701"
   };
Qs.stringify(obj);
console.log(Qs.stringify(obj));
```

如上面代码所示,输出结果如下: 

```
method=query_sql_dataset_data&projectId=85&appToken=7d22e38e-5717-11e7-907b-a6006ad3dba0&datasetId=12564701
```

那么当我们需要传递数组的时候，我们就可以通过下面方式进行处理： 

默认情况下，它们给出明确的索引，如下代码：

```
qs.stringify({ a: ['b', 'c', 'd'] });
// 'a[0]=b&a[1]=c&a[2]=d'
```

也可以进行重写这种默认方式为`false`

```
qs.stringify({ a: ['b', 'c', 'd'] }, { indices: false });
// 'a=b&a=c&a=d'
```

当然，也可以通过`arrayFormat`选项进行格式化输出，如下代码所示：

```
qs.stringify({ a: ['b', 'c'] }, { arrayFormat: 'indices' })
// 'a[0]=b&a[1]=c'
qs.stringify({ a: ['b', 'c'] }, { arrayFormat: 'brackets' })
// 'a[]=b&a[]=c'
qs.stringify({ a: ['b', 'c'] }, { arrayFormat: 'repeat' })
// 'a=b&a=c'
```

在这里需要注意的是，JSON中同样存在stringify方法，但是两者之间的区别是很明显的，如下所示：

```
const Qs = require('qs');
let obj= {
     uid: "cs11",
     pwd: "000000als",
     username: "cs11",
     password: " 000000als"
   };
Qs.stringify(obj);
console.log(JSON.stringify(param));
// '{"uid":"cs11","pwd":"000000als","username":"cs11","password":"000000als"}'
console.log(Qs.stringify(obj));
// 'uid=cs11&pwd=000000als&username=cs11&password=000000als'
```

如上所示，前者是采用JSON.stringify(param)进行处理，后者是采用Qs.stringify(param)进行处理的。

## 3 最佳实践

### 3.1 qs.stringify进阶使用

* 基本用法

`qs.stringify` 则和 `qs.parse` 相反，是把一个参数对象格式化为一个字符串。

```
let params = { c: 'b', a: 'd' };
qs.stringify(params)

// 结果是
'c=b&a=d'
```

* 排序

甚至可以对格式化后的参数进行排序：

```
let params = { c: 'd', a: 'b' };
qs.stringify(params, (a,b) => a.localeCompare(b))

// 结果是
'a=b&c=d'
```

* 指定数组编码格式

``` 
let params = [1, 2, 3];

// indices(默认)
qs.stringify({a: params}, {
    arrayFormat: 'indices'
})
// 结果是
'a[0]=1&a[1]=2&a[2]=3'

// brackets 
qs.stringify({a: params}, {
    arrayFormat: 'brackets'
})
// 结果是
'a[]=1&a[]=2&a[]=3'

// repeat
qs.stringify({a: params}, {
    arrayFormat: 'repeat'
})
// 结果是
'a=1&a=2&a=3'
```

* 处理json格式的参数

在默认情况下，json格式的参数会用 `[]` 方式编码，

```
let json = { a: { b: { c: 'd', e: 'f' } } };

qs.stringify(json);
//结果 'a[b][c]=d&a[b][e]=f'
```

但是某些服务端框架，并不能很好的处理这种格式，所以需要转为下面的格式

```
qs.stringify(json, {allowDots: true});
//结果 'a.b.c=d&a.b.e=f'
```

## 4 同类型技术比较

## 参考资料
   
* [npm-qs](https://www.npmjs.com/package/qs)
* [npm qs 模块(中文)](https://blog.csdn.net/sansan_7957/article/details/82227040)
* [通过script标签引入qs](https://blog.csdn.net/weixin_41769582/article/details/80063517)
* [qs.parse()、qs.stringify()使用方法](https://blog.csdn.net/suwu150/article/details/78333452)
* [qs.js - 更好的处理url参数](https://www.cnblogs.com/small-coder/p/9115972.html)