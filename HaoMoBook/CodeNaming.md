# 代码命名规范

* 方法命名
    * 函数名不能大写
* 注释
    * @TODO代办事项
     

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