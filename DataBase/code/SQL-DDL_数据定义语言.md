# DDL

## 一、数据库操作

1、查询所有数据库

show databases;

2、查询当前数据库

select database();

3、创建数据库

create database (if not exists)数据库名;

4、删除数据库

drop database(if exists)数据库名;

5、使用数据库

use 数据库名;

## 二、表操作

（已经通过use进了数据库）

### 查询

1、查询当前数据库所有表

show tables；

2、查询表结构

dasc 表名；

3、查询指定表的建表语句

### 创建

1、创建表

create table 表名(

字段1 字段1类型[not null(不能为空)] [primary key(设为主键)] [comment ‘ ’],

字段2 字段2类型[comment ‘ ’],

… …

字段n 字段n类型[comment ‘ ’]

)[comment ‘ ’];

(comment ‘ ’表示在’ ‘里写注释)

如图：

![This is a picture](D:\Screenshots\tb_user.png)

### 数据类型

1、数值类型：int（4bytes）、tinyint（1bytes）、double（8bytes）……

注：在double(4,1)中，4代表精度，也就是数据最大多少位，1代表标度也就是小数的位数，如100.5、50.5等

![This is a picture](E:\工具\typora\笔记\DataBase\datas\数值类型.jpg)

2、字符串类型：char、varchar、text、……（前两个要指定长度如char(10)、varchar(10)）

![This is a picture](E:\工具\typora\笔记\DataBase\datas\字符串类型.jpg)

3、日期时间类型

![3f3583a7f925abf0bd3094513d629ad](E:\工具\typora\笔记\DataBase\datas\日期时间类型.jpg)

### 表修改

1、添加字段：alter table 表名 add 字段名 类型(长度);

2、修改字段的数据类型：alter table 表名 modify 字段名 新数据类型(长度);

3、修改字段名和字段类型：alter 表名 change 旧字段名 新字段名 类型(长度);

4、删除字段：alter table 表名 drop 字段名

5、修改表名：alter table 表名 rename to 新表名

6、删除表：

(1)、删除表：drop table 表名

(2)、删除表，并重新创建该表：truncate table 表名
