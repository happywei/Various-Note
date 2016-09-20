
---

## 第二章 关系模型介绍

### 2.1 关系数据库的结构
- 1、**关系(relation)**，用来指代表。
- 2、**元组(tuple)** 用来指代行。
- 3、**属性(attribute)** 指代的是表中的列。
- 4、**关系实例(relation instance)** 表示一个关系的特定实例，也就是所包含的一组特定的行
- 5、如果域中元素被看做是不可再分的单元，则域是 **原子的(atomic)**

### 2.2 数据库模式
- 1、**数据库模式(database schema)** :数据库的逻辑设计。
- 2、**数据库实例(database instance)** 给定时刻数据库中数据的一个快照。
- 3、在关系模式中使用相同属性，正式将不同关系的元组联系起来的一种方法。

### 2.3 码
- 1、**超码(superkey)** ：是一个或多个属性的集合，这些属性的组合可以使我们在一个关系中唯一地标识一个元组。
- 2、**候选码(candidate key)** ：最小超码。
- 3、**主码(primary key)** ：被数据库设计者选中的，主要用来在一个关系中区分不同元组的候选码。
- 4、习惯上把一个关系模式的主码属性列在其他属性前面。
- 5、一个关系模式(r1)可能在它的属性中包括另一个关系模式(r2)的主码。这个属性在r1上称作参照r2的**外码(foreign key)**。关系r1也称为外码依赖的**参照关系(referencing relation)**。r2叫做外码的**被参照关系(referenced relation)**

### 2.4 模式图
- 1、一个含有主码和外码依赖的数据库模式可以用**模式图(schema diagram)** 来表示。
- 2、模式图显示了数据库中的关系，关系的属性，主码和外码。

### 2.5 关系查询语言
- 1、**关系查询语言(relational query language)** 定义了一组运算集，这些运算可以作用于表上，并输出表作为结果。这些运算可以组合成表达式，表达所需的查询。

### 2.6 关系运算
- 1、**连接** ：把分别来自两个悬系的元组合并成单个元组
- 2、**笛卡尔积**：从两个关系中合并元组，但不同于连接运算的是，其结果包含来自两个关系元组的所有对，无论他们的属性值是否匹配。
- 3、**关系代数(relational algebra)** ：提供了一组运算，他们以一个或多个关系为输入，返回一个关系作为输出。诸如SQL这样的实际查询语言是基于关系代数的，但增加了一些有用的语法特征。

---

## 第三章 SQL

### 3.1 SQL查询语言概览

#### SQL 语言的几部分
- 1、**数据定义语言(Data-Definition Language, DDL)** ：SQL DDL提供定义关系模式，删除关系以及修改关系模式的命令。
- 2、**数据操纵语言(Data-Manipulation Language, DML)** ：SQL DML 提供从数据库中查询信息，以及在数据库中插入元组，删除元组，修改元组的能力。
- 3、**完整性(integrity)** ：SQL DDL包括定义完整性约束的命令，保存在数据库中的数据必须满足所定义的完整性约束。破坏完整性约束的更新是不允许的。
- 4、**视图定义(view definition)** ：SQL DDL包括定义视图的命令。
- 5、**事务控制(transaction control)** ：SQL包括定义事务的开始和结束的命令。
- 6、**嵌入式SQL和动态SQL(embedded SQL and dynamic SQL)** ： 嵌入式和动态SQL定义SQL语句如何嵌入到通用编程语言中，如c, cpp, c#
- 7、**授权(authorization)** ：SQL DDL包括定语对关系和视图的访问权限的命令。

### 3.2 SQL数据定义
- 1、基本类型
- - char, varchar, int amallint, numeric, real, double precision, float等
- 2、基本模式定义
- - create table
- - primary key
- - foreign key...references
- - not null
- - insert
- - delete from 从关系中删除元组
- - alter table 为关系增加属性

### 3.3 SQL查询的基本结构

#### 3.3.1 单关系查询

单关系查询
```
select name from instructor
select dept_name from instructor
```

强行删除重复，在select后加入distinct

```
select distinct dept_name from instructor
```
select子句可以带有算数表达式，运算对象可以是常数或元组的属性

```
select ID, name, dept_name, salary * 1.1 from instructor
```
where子句允许我们只选出那些在from子句的结果关系中满足特定谓词的元组。
SQL允许在where子句中使用逻辑连接词and, or, not

```
select name
from instructor
where dept_name = 'Comp. Sci.' and salary > 70000
```

#### 3.3.2 多关系查询

- 1、在理解SQL语句时，最好先从from, 然后where，然后select
```
select name, instructor.dept_name, building
from instructor, department
where instructor.dept_name = department.dept_name
```

- 2、通常来说，一个SQL查询的含义可以理解如下
- - (1) 为from子句中列出的关系产生笛卡尔积
- - (2) 在步骤1的结果上应用where子句中指定的谓词
- - (3) 对于步骤2结果中的每个元组，输出swlect子句中指定的属性(或表达式的结果)

#### 3.3.3 自然连接
- 1、**自然连接(natural join)** ：作用于两个关系，并产生一个关系作为结果。
- 2、自然连接只考虑在两个关系模式中都出现的属性上取值相同的元组对。

```
select name, course_id
from instructor, teaches
where instructor.ID = teaches.ID

也可以这么写

select name, course_id
from instructor natural join teaches
```

### 3.4 附加的基本运算

#### 3.4.1 更名运算
- 1、as子句 old-name as new-name

```
对大学中所有讲授课程的教师，找出他们的姓名以及所讲述的所有课程标识

as 把一个长的名，替换成一个短的。

select T.name, S.course_id
from instructor as T, teaches as S
where T.ID = S.ID
```
- 2、重命名关系的另一个原因是为了适用于需要比较同一个关系中的元组的情况。


```
找出满足下面条件的所有教师的姓名，他们的工资至少比Biology系某一个教师的工资要高

select distinct T.name
from instructor as T, instructor as S
where T.salary > S.salary and S.dept_name = 'Biology'
```

#### 3.4.2 字符串运算
- 1、字符串上可以使用**like**操作符来实现模式匹配。
- - 百分号(%) ：匹配任意字符串
- - 下划线(_) ：匹配任意一个字符

```
找出所在建筑名称中包含字串'Watson'的所有系名

select dept_name
from department
where building like '%Watson%'
```

- 2、SQL允许定义转义字符，在**like** 比较运算中使用 **escape** 关键词来定义转义字符

```
匹配所有以“ab%cd”开头的字符串
like 'ab\%cd%' escape '\'

匹配所有以“ab\cd”开头的字符串
like 'ab\\cd%' escape '\'

使用not like 搜寻不匹配项
select dept_name
from department
where building not like '%Watson%'
```

- 3、SQL：1999还提供**similar to**操作，模式定义语法类似于正则表达式

#### 3.4.3 select子句中的属性说
- 1、星号"*"， 可以用在select子句中表示“所有的属性”

```
select I.*
from instructor as I, teaches as T
where I.ID = T.ID
```
#### 3.4.4 排列元组的显示顺序
- 1、**order by** 子句可以让查询结果中元组按排列顺序显示，默认是升序排列

```
按字母顺序列出在Physics系的所有教师

select name
from instructor
where dept_name = 'Physics'
order by name;
```
- 2、要说明排序顺序，使用**desc** 表示降序，或者用**asc**表示升序


```
按照salary的降序列出整个instructor关系，如果有几位教师工资相同，就将姓名升序排列

select *
from instructor
order by salary desc, name asc
```
#### 3.4.5 where子句谓词
- 1、SQL提供**between**比较运算来说明一个值是小于或等于某个值，同时大于或等于另一个值的。

```
找出工资在90000和100000之间的教师的姓名

select name 
from instructor
where salary between 90000 and 100000

它可以取代

select name
from instructor 
where salary <= 100000 and salary >= 90000

当然还有not between 运算符

```

- 2、SQL允许我们用几号(v1, v2...)来表示一个分量值分别为v1, v2...的n维元组，在元组上可以运用比较运算符，按字典顺序进行比较运算。


```
查找Biology系讲授了课程的所有教师姓名和他们所讲授的课程

select name, course_id
from instructor, teaches
where instructor.ID = teaches.ID and dept_name = 'Biology';

可以被重写成这种形式

select name, course_id
from instructor, teaches
where (instructor.ID, dept_name) = (teachers.ID, 'Biology');

```

---
### 3.5 集合运算
- 1、SQL作用在关系上的**union, intersect, except** 运算，对应于并集，交集，差。

```
在2009年秋季学期开设的所有课程的集合
select course_id
from section
where semester = 'Fall' and year = 2009;

在2010年春季学期开设的所有课程的集合
select course_id
from section 
where semester = 'Spring' and year = 2010;
```

3.5.1 并运算


```
找出在2009年秋季学期和2010年春季学期都开设的所有课程

(select course_id
from section
where semester = 'Fall' and year = 2009)
union
(select course_id
from section 
where semester = 'Spring' and year = 2010)
```

**union** 运算自动去除重复，想要保留重复要使用**union all** 来代替**union**

```
找出在2009年秋季学期和2010年春季学期都开设的所有课程

(select course_id
from section
where semester = 'Fall' and year = 2009)
union all   
(select course_id
from section 
where semester = 'Spring' and year = 2010)
```



















