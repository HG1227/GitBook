# Moment

#### 作者：高天阳
#### 邮箱：13683265113@163.com

```
更改历史

* 2018-8-15	    高天阳      初始化文档

```
## 1. 简介

### 1.1 什么是Moment

Moment旨在在浏览器和Node.js中工作。

目前，以下浏览器用于ci系统：Windows 7上的IE8，IE9，Windows XP上的稳定Chrome，
Mac上的Safari 10.8和Linux上的稳定Firefox。

所有代码都适用于这两种环境。所有单元测试都在两种环境中运行。

moment.js不依赖任何第三方库，支持字符串、Date、时间戳以及数组等格式，
可以像PHP的date()函数一样，格式化日期时间，计算相对时间，获取特定时间后的日期时间等等。

## 2. 安装和使用

### 2.1 安装

#### 2.1.1 Node.js

```
npm install moment
```

```
var moment = require('moment');
moment().format();
```

* 注意：在`2.4.0`版本，不推荐使用全局导出的时刻对象。它将在下一个主要版本中删除。

#### 2.1.2 script标签引入

```
<script src="moment.js"></script>
<script>
    moment().format();
</script>
```

* 注意：`Moment.js`可在`cdnjs.com`上找到。但请记住将他们的`script`标签串联以最小化http请求。

#### 2.1.3 Bower

```
bower install --save moment
```

* 注意：moment.js，locale/*.js和min/moment-with-locales.js。

#### 2.1.4 Require.js

```
require.config({
    paths: {
        "moment": "path/to/moment",
    }
});
define(["moment"], function (moment) {
    moment().format();
});
```

Moment仍将创建一个`moment`全局，这对插件和其他第三方代码很有用。如果您希望压缩全局，请使用`noGlobal`模块配置中的选项。

```
require.config({
    config: {
        moment: {
            noGlobal: true
        }
    }
});
```

如果未指定，`noGlobal`则全局导出的时刻将打印弃用警告。从下一个主要版本开始，如果你想要这种行为，你必须自己导出它。

对于版本`2.5.x`，如果您使用其他依赖Moment但不兼容AMD的插件，则可能需要添加`wrapShim: true` 到`r.js`配置中。

* 注意：要允许在requirejs环境中加载moment.js插件，请将时刻创建为命名模块。正因为如此，时刻必须被加载完全一样的"moment"，用paths确定的目录。需要时刻与路径一样"vendor\moment"将返回undefined。

* 注意：从版本2.9.0开始，将自身导出为匿名模块，因此如果您只使用核心（没有区域设置/插件），那么如果将其放在非标准位置，则不需要配置。

#### 2.1.5 NuGet

```
Install-Package Moment.js
```

#### 2.1.6 spm

```
spm install moment --save
```

#### 2.1.7 meteor

```
meteor add momentjs:moment
```

### 2.2 使用

`Date.prototypeMoment.js` 不是修改本机日期，而是为`Date`对象创建一个包装器。
要获取此包装器对象，只需`moment()`使用其中一种受支持的输入类型进行调用即可。

该`Moment`原型是通过暴露`moment.fn`。如果你想添加自己的功能，那就是你要放置它们的地方。

为便于参考，`Moment.prototype`将在文档中引用任何方法`moment#method`。
所以`Moment.prototype.format`=== `moment.fn.format`=== `moment#format`。

#### 2.2.1 格式化时间

#### 2.2.2 相对时间

#### 2.2.3 加减时间

#### 2.2.4 多语言支持

----------

#### 2.2.1 当前时间 `1.0.0+`

```
moment();
```

要获取当前日期和时间，只需moment()使用无参数调用即可。

```
var now = moment();
```

这与调用`moment(new Date())`基本相同。

#### 2.2.2 字符串 `1.0.0+`

```
moment(String);
```

从字符串创建时刻时，我们首先检查字符串是否与已知的[ISO 8601](https://en.wikipedia.org/wiki/ISO_8601)格式匹配，
然后在`new Date(string)`找不到已知格式时返回。

```
var day = moment("1995-12-25");
```

* 警告：浏览器对解析字符串支持[不一致](http://dygraphs.com/date-formats.html)。
由于没有关于应支持哪种格式的规范，因此在某些浏览器中有效的功能将无法在其他浏览器中使用。

为了解析除ISO 8601字符串以外的任何其他内容的一致结果，
您应该使用[String + Format](http://momentjs.cn/docs/#/parsing/string-format/)。

##### 支持的ISO 8601字符串

ISO 8601字符串需要日期部分。

```
2013-02-08  # A calendar date part
2013-W06-5  # A week date part
2013-039    # An ordinal date part
```

还可以包括时间部分，通过空格或大写T与日期部分分开。

```
2013-02-08T09            # An hour time part separated by a T
2013-02-08 09            # An hour time part separated by a space
2013-02-08 09:30         # An hour and minute time part
2013-02-08 09:30:26      # An hour, minute, and second time part
2013-02-08 09:30:26.123  # An hour, minute, second, and millisecond time part
2013-02-08 24:00:00.000  # hour 24, minute, second, millisecond equal 0 means next day at midnight
```

任何日期部分都可以包含时间部分。

```
2013-02-08 09  # A calendar date part and hour time part
2013-W06-5 09  # A week date part and hour time part
2013-039 09    # An ordinal date part and hour time part
```

如果一个时间部分被包括，一个从UTC偏移量也可被包括为`+-HH:mm`，`+-HHmm`，或`Z`。

```
2013-02-08 09+07:00            # +-HH:mm
2013-02-08 09-0100             # +-HHmm
2013-02-08 09Z                 # Z
2013-02-08 09:30:26.123+07:00  # +-HH:mm
```

* 注意：*1.5.0*版中添加了自动跨浏览器ISO-8601支持。版本*2.3.0*中添加了对星期和序数格式的支持。
如果字符串与上述任何格式都不匹配且无法解析`Date.parse`，`moment#isValid`则返回false。

```
moment("not a real date").isValid(); // false
```

#### 2.2.3 字符串+格式 `1.0.0+`

```
moment(String, String);
moment(String, String, String);
moment(String, String, Boolean);
moment(String, String, String, Boolean);
```

如果您知道输入字符串的格式，可以使用它来解析片刻。

```
moment("12-25-1995", "MM-DD-YYYY");
```

解析器忽略非字母数字字符，因此以下两个都将返回相同的内容。

```
moment("12-25-1995", "MM-DD-YYYY");
moment("12/25/1995", "MM-DD-YYYY");
```

解析令牌类似于使用的格式化令牌`moment#format`。

##### 年，月，日缩写

| 输入 | 输出 | 描述 |
|:---:|:----:|:---:|
| `YYYY`| `2014` | 4或2位数年份 |
| `YY`| `14` | 2位数年份 |
| `Q`| `1..4` | 一年四分之一。将季度设置为季度的第一个月。 |
| `M MM`| `1..12` | 月份编号 |
| `MMM MMMM`| `Jan..December` | 设置的语言环境中的月份名称 moment.locale() |
| `D DD`| `1..31` | 一个月的一天 |
| `Do`| `1st..31st` | 有序的月份日 |
| `DDD DDDD`| `1..365` | 一年的一天 |
| `X`| `1410715640.579` | Unix时间戳 |
| `x`| `1410715640579` | Unix ms时间戳 |

`YYYY`从版本`2.10.5`支持2位数年份，并将它们转换为2000年附近的一年（相同`YY`）。

##### 周年，周和工作日缩写

对于这些，小写标记使用区域设置感知周开始日期，而大写标记使用[ISO](https://en.wikipedia.org/wiki/ISO_week_date)周日期开始日期。

| 输入 | 输出 | 描述 |
|:---:|:----:|:---:|
| `gggg`| `2014` | Locale 4位数周 |
| `gg`| `14` | Locale 2位数周 |
| `w ww`| `1..53` | 一年中的地方周 |
| `e`| `1..7` | 区域日期 |
| `ddd dddd	`| `Mon...Sunday` | 设置的语言环境中的月份名称 moment.locale() |
| `GGGG`| `2014` | ISO 4位数周 |
| `GG`| `14` | ISO 2位数周 |
| `W WW`| `1..53` | ISO周一年 |
| `E	`| `1..7` | ISO星期几 |

##### 小时，分钟，秒，毫秒和偏移缩写

| 输入 | 输出 | 描述 |
|:---:|:----:|:---:|
| `H HH	`| `0..23` |24小时的时间|
| `h hh	`| `1..12` |使用12小时的时间a A。|
| `a A	`| `am pm` |张贴或赌注meridiem|
| `m mm	`| `0..59` |分钟|
| `s ss	`| `0..59` |秒|
| `S`| `0..9` |十分之一秒|
| `SS`| `0..99` |百分之一秒|
| `SSS`| `0..999` |千分之一秒|
| `SSSS`| `0000..9999` |毫秒|
| `Z ZZ	`| `+12:00` |从UTC偏移量+-HH:mm，+-HHmm或Z|

从版本`2.10.5`：小数秒标记长度4到9可以解析任意数量的数字，但只考虑前3（毫秒）。如果您有时间打印了许多小数位并想要消耗输入，请使用。

还可以使用区域设置感知日期和时间格式`LT LTS L LL LLL LLLL`。它们是在`2.2.1`版本中添加的，除了`LTS`增加了 `2.8.4`。

`Z ZZ`在版本中添加`1.2.0`。

`S SS SSS`在版本中添加`1.6.0`。

`X`在版本中添加`2.0.0`。

除非指定时区偏移量，否则解析字符串将在当前时区中创建日期。

```
moment("2010-10-20 4:30",       "YYYY-MM-DD HH:mm");   // parsed as 4:30 local time
moment("2010-10-20 4:30 +0000", "YYYY-MM-DD HH:mm Z"); // parsed as 4:30 UTC
```
如果由解析的输入产生的时刻不存在，`moment#isValid`则返回false。

```
moment("2010 13",           "YYYY MM").isValid();     // false (not a real month)
moment("2010 11 31",        "YYYY MM DD").isValid();  // false (not a real day)
moment("2010 2 29",         "YYYY MM DD").isValid();  // false (not a leap year)
moment("2010 notamonth 29", "YYYY MMM DD").isValid(); // false (not a real month name)
```

从版本开始`2.0.0`，可以将区域设置键作为第三个参数传递给`moment()`和`moment.utc()`。

```
moment('2012 juillet', 'YYYY MMM', 'fr');
moment('2012 July',    'YYYY MMM', 'en');
```

Moment的解析器非常宽容，这可能会导致不良行为。从版本开始`2.3.0`，您可以为最后一个参数指定一个布尔值，
以使Moment使用严格的解析。严格的解析要求格式和输入完全匹配。

```
moment('It is 2012-05-25', 'YYYY-MM-DD').isValid();       // true
moment('It is 2012-05-25', 'YYYY-MM-DD', true).isValid(); // false
moment('2012-05-25',       'YYYY-MM-DD', true).isValid(); // true
```

您可以同时使用区域设置和严格性。

```
moment('2012-10-14', 'YYYY-MM-DD', 'fr', true);
```

##### 解析两位数年份

默认情况下，68岁以上的两位数年份假定为1900年，68年或以下年份假定为2000年。可以通过替换`moment.parseTwoDigitYear`方法来更改此设置。

#### 2.2.4 字符串 `1.0.0+`

```
```

#### 2.2.5 字符串 `1.0.0+`

```
```

#### 2.2.6 字符串 `1.0.0+`

```
```

#### 2.2.7 字符串 `1.0.0+`

```
```






## 参考资料

* [Moment.js 文档](http://momentjs.cn/docs/)
* [使用moment.js轻松管理日期和时间](https://blog.csdn.net/yelin042/article/details/77878288)