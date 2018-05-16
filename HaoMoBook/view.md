# 创建视图说明 {#toc_0}

作者：乔继超

邮箱:qiaojichao@haomo-studio.com

## 现有如下两张表：

1.年级表（ID，年级名称）

![](../assets/grade.jpg)

2.学生表（ID，姓名，年龄，地址，年级）

![](../assets/student.jpg)


## 现在要满足以下需求

```
创建一张视图，要求这个视图把学生表和年级表的信息都带出来，通过查询这张视图返回学生信息和所对应的年级信息。
```

## 注意

```
若要多表关联，相互关联的两张表之间必须存在关联字段！

再次案例中，关联字段是学生表中的“grade_id”,通过学生表中的“grade_id”找到年级表中的主键ID带出数据

```
![](../assets/guanxi.jpg)


## 创建视图

创建视图的基本语句：
```
CREATE VIEW view_name（视图名称）
AS sql查询语句

```

创建学生表和年级表的视图：
```
CREATE VIEW student_grade_view
AS select stu.*,gra.* from student as stu INNER join grade as gra on stu.grade_id=gra.id

注意：‘as’指的是另起一个别名

上述语句展示信息为学生表所有字段和年级表的所有字段(因为都是*)

那么就存在一个问题：两张表共同存在的字段就会重名

怎么解决呢？

第二张表的字段用‘表名.字段名’的方式进行展示，这样就可以给字段名其别名了

那么修改后的语句就是：

CREATE VIEW student_grade_view
AS select stu.*,gra.id as gra_id,gra.grade_name as gra_gradeName from student as stu INNER join grade as gra on stu.grade_id=gra.id

```
![](../assets/view.jpg)

