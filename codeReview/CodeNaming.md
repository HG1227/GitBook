# 项目命名规范

## class命名规范

### 网页内容类：
* 标题：title
* 摘要：summary
* 箭头：arrow
* 商标：label
* 网站标志：logo
* 转角/圆角：corner
* 横幅广告：banner
* 子菜单：subMenu
* 搜索：search
* 搜索框：searchBox
* 登录：login
* 登录条：loginbar
* 工具条：toolbar
* 下拉：drop
* 标签页：tab
* 当前的：current
* 列表：list
* 滚动：scroll
* 服务：service
* 提示信息：msg
* 热点：hot
* 新闻：news
* 小技巧：tips
* 下载：download
* 栏目标题：title
* 加入：joinus
* 注册：regsiter
* 功能区：shop
* 加入：joinus
* 状态：status
* 按钮：btn
* 图标：icon
* 注释：note
* 指南：guild
* 投票：vote
* 合作伙伴：partner
* 友情链接：link
* 版权：copyright

### class命名：
* 颜色：使用颜色的名称或16进制码

```
.red{color:red;}
.f60{color:#f60}
.ff8600{color:#ff8600}
```

* 字体大小，直接使用“font+字体大小”
    
```
.font12px{font-size:12px}
.font9pt{font-size:9pt}
```

* 对其样式，使用对齐目标的英文名称

```
.left{float:left;}
.bottom{float:bottom;}
```
* 标题栏样式，使用“类别+功能”的方式命名

```
.barnews{}
.barproduct{}
```
* 注意：

1. 一律小写
2. 尽量英文
3. 不加中杠或下划线
4. 尽量不缩写，除非一看就明白

### 推荐css书写顺序

* 显示属性
    * display
    * list-style
    * position
    * float
    * clear

* 自身属性
    * width
    * height
    * margin
    * padding
    * border
    * background

* 文本属性
    * color

## js命名规范

* 方法命名
    * 函数名不能大写
* 注释
    * @TODO代办事项
    * 注释方法 /**回车
```
/**
* @TODO @desc 需要修改函数名称
* @params
* @return
*/
```
     

var  vm = $scope.vm = {}
vm.search = fucntion(){}

代码可读性，规法
不要在controller里写逻辑
可以写个方法 调用
before enter监听事件是否处理完

传参
vm.search = JSON.parse(JSON.stringify(statesParams))
vm.setFilters = function(){}
VM.SEARCH = function(){}
vm.process = fucntion(){}

retrun vm.search.cg-cuurentpge<=1
$q.all异步执行
页面上要显示的变量要写在前面  不然会报错
传入的参数要进行判断 假设不存在会不会发生异常
select ng-options  = "item.id as item.name item in items"

filters  过滤值  应该定义一个公共的方法

3. 可读性，一行<80;
4. 事件，加载before。。。。
5. 变量最少化
6. 代码加注释
7. 变量声明放
8. 先处理异常，代码尽量左边靠