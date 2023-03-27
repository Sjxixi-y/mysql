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































