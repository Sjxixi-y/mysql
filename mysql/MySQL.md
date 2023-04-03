# MySQL

## 一、简介

> 按照数据结构来组织、存储和管理数据的仓库。是一个长期存储在计算机内的、有组织的、有共享的、统一管理的数据集合。



**关系型数据库：**表之间相互有关系

**非关系型数据库：**表之间没有关系。多使用哈希表，表中以键值对的方式储存。



**术语**：

**数据库：**数据库是长期保存在计算机存储设备上的、有组织或按一定格式存放的、可以共享的数据集合 

**数据库管理系统：**建立在操作系统的基础上，对数据库进行统一管理和控制的软件。

**数据库系统：**由数据库和数据库管理系统组成。



## 二、数据库操作

CRUD ：增删改查



### 1. 查询所有数据库

```sql
show databases;
```



### 2. 创建数据库

```sql
-- 创建数据库，'name' 为数据库名字
create database <name> ;
-- 指定数据库编码，需要出现在创建数据库之后。
default character set utf8;
```



### 3. 查看指定数据库

```sql
-- 查看数据库的信息
show create database <name>;
```



### 4. 删除数据库

```java
drop database <name>;
```



### 5. 修改数据库

```sql
-- default 在当前表示默认字符集
alter database day15 default character set gbk;
-- 修改数据库的字符集
alter database <name> character set utf8; # utf8 gbk;
```



### 6. 查看当前使用的数据库

```sql
select database();
```



### 7. 切换使用的数据库

```sql
use <name>;
```



## 三、表管理

### 1. 查看所有表

```sql
show tables;
```



### 2. 创建表

```sql
CREATE TABLE employee(
	id INT,
	NAME VARCHAR(20),
	gender VARCHAR(2),
	birthday DATE,
	email VARCHAR(10),
	remark VARCHAR(50)
);
```



### 3. 查看表结构

```java
desc <name>;
```



### 4. 删除表

```sql
drop table <name>;
```



### 5. 修改表

#### 5.1 添加字段

```sql
-- alter table 表示要修改一个表结构
-- add column 表示添加一个 列
-- neme2 表示新的列的名字
alter table <name> add column <name2> varchar(2);
```



#### 5.1 删除字段

```sql
-- alter table 表示要修改一个表结构
-- drop column 表示删除一个 列
alter table <name> drop column <name>;
```



#### 5.3 修改字段类型

```sql
-- modify column 修改列类型
alter table <name> modify column <name> varchar(100);
```



#### 5.4 修改字段名称

```sql
-- 指定新的名字与类型
-- change column 修改列名字
alter table <name> change column <name> <name> varchar(2);
```



#### 5.5 修改表名称

```sql
-- rename to 表示 改名为
alter table <name> rename to <name>;
```



## 四、常用数据类型

|     类型     |   表示    |        格式         |
| :----------: | :-------: | :-----------------: |
|     整形     |    int    |          1          |
|    浮点型    |  double   |         1.0         |
|    字符串    |  varcahr  |       abcdeaf       |
|     日期     |   date    |     2023-03-27      |
|     时间     |   time    |      11:12:13       |
|     年份     |   year    |        2023         |
| 年日月时分秒 | datetime  | 2023-03-27 11:12:13 |
|    时间戳    | timestamp |   20230327111213    |

## 五、增删改

### 1. 添加数据

**1.1 添加一行数据** 

```sql
insert into <name> values(null, "白云", "张", "1980-01-11", "123-1234-1234", "abcd", "长沙", "岳麓", 2000);
```



**1.2 选择性添加输入** 

```sql
insert into <name>(first_name, last_name, address, city, state, points) 
values("jack", "chen", "asdasd", "a", "ac", 12346); -- 属性
```



**1.3 添加多行数据** 

```sql
insert into <name>(first_name, last_name, birth_date, phone, address, city, state, points)
values -- 属性
	("建国","王","1985-10-01","12312312312","abab"," ","岳塘",2000),
	("建军","王","1985-10-01","12346579465","abab","湘潭","岳塘",3000),
	("建党","王","1985-10-01","12364687451","abab","湘潭","岳塘",2500),
	("建业","王","1985-10-01","13520165210","abab","湘潭","岳塘",5000);
```



**1.4  同时对多个表添加相同数据**

last_insert_id() -- 获取上一次操作自动添加的主键值。用于添加另一个表。

```sql
insert into <name>(customer_id, order_date, status) values (5, "2019-01-20", 1);

insert into <name>(order_id, product_id, quantity, unit_price) values(last_insert_id(), 2, 4, 3.11);
```



**1.5 备份表**

* 新建表

```sql
create table <name2> select * from <name>;
```

* 添加数据

```sql
insert into <name2> select * from <name>;
```

* 有条件的添加数据

```sql
insert into <name2> select * from <name> where order_id = 1;
```

name2 表示 备份的表名。



### 2. 改变数据

```sql
update <name> set order_date = "2019-03-14", customer_id = 1 where order_id = 1;
```



### 3. 删除数据

3.1 条件删除

```sql
delete from <name> where order_id = 1;
```



3.2 删除所有数据

```sql
delete from <name>;
```



3.3 删除表后新建

```sql
truncate table
```



## 六、查询

### 1. 单表查询

#### 1.1 选择指定的列显示

```sql
Select [目标列], [目标列], [目标列] … from <name>
```



#### 1.2 对指定的列拼接

```sql
Select [目标列]+[目标列], [目标列] * 8 … from <name>
```



#### 1.3 对拼接的列赋予别名

```sql
Select [目标列], [目标列]+[目标列] as <name> … from <name>
```



#### 1.4 别名是中文无需打单引号，但中文中含有空格必须打单引号

```sql
Select [目标列], [目标列]+[目标列] as '<别<空格>名>' from <name>
```



#### 1.5 使用修饰符去重

```sql
Select distinct <目标列> from <name>
```



### 2. 条件查询

#### 2.1 大于、小于、等于

```sql
select * from <name> where customer_id = 2;
```



#### 2.2 条件组合判断。And(且)，or(或)，not(取反)

```sql
-- 大于2 & 小于5，不包括
select * from customers where customer_id > 2 and customer_id < 5;
-- 小于3 | 大于8，不包括
select * from customers where customer_id < 3 or customer_id > 8;
-- 大于5的反面，小于等于5
select * from customers where not(customer_id > 5 );
```



#### 2.3 表示固定范围。In

```sql
-- 选择1、5、7、10。
select * from customers where customer_id in (1, 5, 7, 10);
-- 除去1、6、9。
select * from customers where customer_id not in (1, 6, 9);
```



#### 2.4  表示一个区间。Between

```sql
-- 【5，9】
select * from customers where customer_id between 5 and 9;
```



#### 2.5 模糊查询。Like

```sql
-- 找到第二个字母为a的，_ 为 一个任意字符，% 为任意字符
select * from customers where last_name like "_a%";
```



#### 2.6 比较null。 Is

```sql
-- 找到phone中为空的项
select * from customers where phone is null;
-- 找到phone不为空的项
select * from customers where phone is not null;
```



#### 2.7 结果排序。Order by \desc

```sql
-- 正序
select * from customers order by points;
-- 反序
select * from customers order by points desc;
```



#### 2.8 分页查询。 Limit

```sql
-- 表示取前面三行
select * from customers limit 3;
-- 表示去除前面2行取之后的3行，3表示每一页的长度。
select * from customers limit 2, 3;
```



#### 2.9 正则表达式查询

```sql
select * from customers where last_name regexp '^field|mac';
```



#### 2.10 分支结构查询

```sql
// 查询 salary 表，新增一个字段，根据年薪分级。
SELECT
	*,
	CASE 
         WHEN salary > 10000 THEN 'A'
         WHEN salary > 8000 THEN 'B'
         ELSE 'C'
    END AS salary_grade
FROM salary;
```





### 3. 多表查询

**重点：在表后添加的字符都会被视为表达别名。**



#### 3.1 多表简单查询

```sql
select c.*, o.* from customers c inner join orders o;
```



#### 3.2 关联条件。on

```sql
select c.customer_id, o.order_id 
from customers c inner 
join orders o 
on c.customer_id = o.customer_id;
```



#### 3.3 自连接

```sql
--  查询员工表中的普通员工和他的管理者
select e1.*, e2.* from employees e1 
join employees e2 
on e1.reports_to = e2.employee_id;
```



#### 3.4 多表连接 

```sql
-- 查询用户的多个订单，与他们的状态
select c.*, o.*, os.*
from customers c
join orders o on c.customer_id = o.customer_id
join order_statuses os 
on o.`status` = order_status_id;
```



#### 3.5 组合条件

```sql
-- 单一条件无法得出结论，于是多加一条条件
select *
from order_items oi
join order_item_notes oin 
on oi.order_id = oin.order_Id and oi.product_id = oin.product_id;
```



#### 3.6 隐式查询 

```sql
-- 等价于inner jion
select *
from customers c, orders o, order_statuses os
where c.customer_id = o.customer_id and o.`status` = os.order_status_id;
```



#### 3.7 外连接

即使没有数据，依然展示。

- ##### 左连接 `left` 以左表为主

```sql
select c.customer_id, o.order_id, o.order_date
from customers c
left join orders o
on c.customer_id = o.customer_id;
```



- ##### 右连接 `right ` 以右表为主

```sql
-- 与上式结果相同，上式以 customers 表为主，下式同样以 customers 表为主。
select c.customer_id, o.order_id, o.order_date
from orders o
right join customers c
on c.customer_id = o.customer_id;
```



#### 3.8 多表外连接 

```sql
select 
c.customer_id, o.order_id, s.shipper_id
from customers c
left join orders o on c.customer_id = o.customer_id
left join shippers s on o.shipper_id = s.shipper_id
order by c.customer_id;
```



#### 3.9 自外连接 

```sql
select *
from employees ea 
left join employees eb
on ea.reports_to = eb.employee_id;
```



#### 3.10 using从句 

```sql
-- 连接条件不再使用on关键字，而且括号内还能添加更多的值，达成组合条件。
select *
from customers c
join orders o using(customer_id);
```



#### 3.11 自然连接  natural

```sql
-- 由数据库自己判断连接条件
select *
from customers c
natural join orders o
```



#### 3.12 交叉连接 

```sql
-- 不写判断条件，让前表每一条数据都和后表数据结合。
select c.first_name, o.order_id from customers c join orders o;
select c.first_name, o.order_id from customers c, orders o;
```



#### 3.13 联合查询

```sql
-- 将不同来源、结果的表合成一张表
select c1.*, '金牌' as '奖牌' from customers c1 where c1.points >= 3000
union
select c2.*, '银牌' from customers c2 where c2.points >= 2000 and c2.points < 3000
union
select c3.*, '铜牌' from customers c3 where c3.points < 2000;
```



## 七、聚合函数

### 1. 最大值

```sql
select MAX(points) from customers;
```



### 2. 最小值 

```sql
select Min(points) from customers;
```



### 3. 求和 

```sql
select SUM(points) from customers;
```



### 4. 平均值 

```sql
select AVG(points) from customers;
```



### 5. 数量 

```sql
-- 遇到 unll 会不计数
select COUNT(phone) from customers;

-- 换成 * 
select COUNT(*) from customers;

-- 也可以 1、-1、0.....
-- 相当于在每一行添加了一个 0 然后统计数量。
select COUNT(0) from customers;

-- 去重查询
select count(distinct office_id) from employees;
```



## 八、分组查询

### 1. 













DROP 删除对象 

































