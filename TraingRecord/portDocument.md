# 自动化生成接口的使用

## 表结构

![](/assets/portDocument/portDocument1.png)

## 增加数据

![](/assets/portDocument/portDocument2.png)

![](/assets/portDocument/portDocument3.png)

```
http://bcs.hitevision.com/v1/work_reports/new
域名:http://bcs.hitevision.com/v1/
表名复数:work_reports
接口功能:new
X-Auth-Token:7bfbe22249a244b88daf903f951c6481
用户信息:X-Auth-Token
```

## 删除数据

![](/assets/portDocument/portDocument4.png)

```
http://bcs.hitevision.com/v1/work_reports/980beb8304d14e8482f25f0b25e64d63/delete
域名:http://bcs.hitevision.com/v1/
表名复数:work_reports
数据id:980beb8304d14e8482f25f0b25e64d63
接口功能:delete
```

## 修改数据

![](/assets/portDocument/portDocument5.png)

![](/assets/portDocument/portDocument6.png)

```
http://bcs.hitevision.com/v1/work_reports/980beb8304d14e8482f25f0b25e64d63/edit
域名:http://bcs.hitevision.com/v1/
表名复数:work_reports
修改数据id:980beb8304d14e8482f25f0b25e64d63
接口功能:edit
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

### 例子1:查询并有条件

![](/assets/portDocument/portDocument9.png)

```
http://bcs.hitevision.com/v1/work_reports?filters=%7B%22work_report%22%3A%7B%22id%22%3A%7B%22equalTo%22%3A%22980beb8304d14e8482f25f0b25e64d63%22%7D%7D%7D
域名:http://bcs.hitevision.com/v1/
表名复数:work_reports
条件:?filters=%7B%22work_report%22%3A%7B%22id%22%3A%7B%22equalTo%22%3A%22980beb8304d14e8482f25f0b25e64d63%22%7D%7D%7D
```

[编码与解码工具](http://tool.css-js.com/urldecode.html)

![](/assets/portDocument/portDocument10.png)

![](/assets/portDocument/portDocument11.png)

### 例子2:查询并有条件

![](/assets/portDocument/portDocument12-1.png)

![](/assets/portDocument/portDocument12-2.png)

![](/assets/portDocument/portDocument12-3.png)

![](/assets/portDocument/portDocument12-4.png)

## 从外键表查主键表数据

![](/assets/portDocument/portDocument12.png)

* @param includes JSON字符串, 用来将本表的外链字段(table_id类似的字段)指向的外链表的完整行数据返回, 格式为
```
{
    'include_table1': {     外链表 表名1   本表所对应的主键表
        includes: ['include_table11', 'include_table12']  与主表所对应的外键
    },
    'include_table2': {    外链表 表名2
        includes: ['include_table21', 'include_table22']  与主表所对应的外键
    }
}
```

## 从主键表查外键表数据

![](/assets/portDocument/portDocument13.png)

* @param refers JSON字符串, 用来将其他表的外链字段为本表的表数据返回, 格式为
```
{
    'refer_table1': {        主键id所对应的外键表 表名1  本表所对应的外键表
        includes: ['include_table11', 'include_table12']   外键表的外键字段
    },
    'refer_table2': {        主键id所对应的外键表 表名2
        includes: ['include_table21', 'include_table22']   外键表的外键字段
    }
}
```

### 例子:

![](/assets/portDocument/portDocument14.png)

* filters

![](/assets/portDocument/portDocument15.png)

* refers

![](/assets/portDocument/portDocument16.png)

## 两个表没主外键关系但值相同

![](/assets/portDocument/portDocument17.png)

* @param relates JSON字符串, 用来将其他有间接关系的表(所谓间接关系, 一定是跟本表的某个字段名一致, 且指向同一张表),两张表中非主键的两个字段相等
```
{
    'relate_table1': ['column1', 'column2'],    '关联的另一张表名':['一致的字段名']   
    'relate_table1': ['column3', 'column4']
}
```

* 主键: 主键是能确定一条记录的唯一标识，自动生成的主键为id
* 外键: 外键用于与另一张表的关联。是能确定另一张表记录的字段，用于保持数据的一致性
* 查询列表接口名称:为表名的复数形式