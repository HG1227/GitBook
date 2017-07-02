# 自动化生成接口的使用

## 表结构

![](/assets/portDocument/portDocument1.png)

## 增加数据

![](/assets/portDocument/portDocument2.png)

![](/assets/portDocument/portDocument3.png)

```
http://bcs.hitevision.com/v1/work_reports/new
http://bcs.hitevision.com/v1/：域名
work_reports:表名复数
new:接口功能
X-Auth-Token:7bfbe22249a244b88daf903f951c6481
X-Auth-Token:用户信息
```

## 删除数据

![](/assets/portDocument/portDocument4.png)

```
http://bcs.hitevision.com/v1/work_reports/980beb8304d14e8482f25f0b25e64d63/delete
http://bcs.hitevision.com/v1/：域名
work_reports:表名复数
980beb8304d14e8482f25f0b25e64d63:数据id
delete:接口功能
```

## 修改数据

![](/assets/portDocument/portDocument5.png)

![](/assets/portDocument/portDocument6.png)

```
http://bcs.hitevision.com/v1/work_reports/980beb8304d14e8482f25f0b25e64d63/edit
http://bcs.hitevision.com/v1/:域名
work_reports:表名复数
980beb8304d14e8482f25f0b25e64d63:修改数据id
edit:接口功能
```

## 查询数据

* @param pageNo(写成条件为:page_no)          整数,如1           起始页页数
* @param pageSize(写成条件为:page_size)      整数,如10          每页显示条数
* @param sortItem(写成条件为:sort_item)      格式为"id, name"   根据字段排序  (sortItem与sortOrder一一对应)
* @param sortOrder(写成条件为:sort_order)    格式为"asc, desc"  排序的关键字  (asc正序,desc倒叙)

### 例子:
查询并分页显示、从第1页显示、每页1条数据

![](/assets/portDocument/portDocument7.png)

查询并分页显示、从第1页显示、每页5条数据、按id正序排序

![](/assets/portDocument/portDocument8.png)

## 单表查询条件
* @param filters JSON字符串, 用来过滤列表的数据, 格式为
```
{
    'table':    表名
        {
        'column1': {                            表中的字段
        like: '%abc%',                          模糊查询,包含字符”abc”
        notLike: ''                             模糊查询,不包含字符
        between: [1, 10],                       取值在[1,10]之间,包含1与10
        notBetween: [1, 10]                     取值小于1大于10
        isNull: true,       // 只能为true       判断字段是否为空
        isNotNull: true,    // 只能为true       判断字段是否不为空
        equalTo: "abc",                         相等于
        notEqualTo: "abc",                      不等于
        greaterThan: 10,                        大于
        greaterThanOrEqualTo: 10,               大于等于
        lessThan: 10,                           小于
        lessThanOrEqualTo: 10,                  小于等于
        in: [],                                 包含[]中字段
        notIn: []                               不包含[]中字段
        }
    }
}
```

### 例子:查询并有条件

![](/assets/portDocument/portDocument9.png)

```
http://bcs.hitevision.com/v1/work_reports?filters=%7B%22work_report%22%3A%7B%22id%22%3A%7B%22equalTo%22%3A%22980beb8304d14e8482f25f0b25e64d63%22%7D%7D%7D
http://bcs.hitevision.com/v1/:域名
work_reports:表名复数
?filters=%7B%22work_report%22%3A%7B%22id%22%3A%7B%22equalTo%22%3A%22980beb8304d14e8482f25f0b25e64d63%22%7D%7D%7D:条件
```

[编码与解码工具](http://tool.css-js.com/urldecode.html)

![](/assets/portDocument/portDocument10.png)

![](/assets/portDocument/portDocument11.png)





