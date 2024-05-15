# 存储引擎

## MySQL体系结构

> 连接层
>
> 服务层
>
> 引擎层
>
> 存储层

## 存储引擎简介

mysql5.5后默认存储引擎为InnoDB

```mysql
-- 查询建表语句
show create table 表名;
-- 指定存储引擎
create table 表名(
    ......
)engine=存储引擎;
-- 查看数据库支持的存储引擎
show engines;
```

## 存储引擎特点

1、innoDB：

> 特点：事务、外键、行级锁
>
> 文件：表名.ibd,参数为innodb_file_per_table,用于决定多表共用表空间文件还是单表使用一个表空间文件，打开的说明一张表对应一个表空间文件，查询语句为：show variables like ‘innodb_file_per_table’;
>
> 逻辑存储结构：tablespece：表空间、segment：段、extent：区、page：页、row：行(自大向小包含)

2、mylsam：

> 不支持事务
>
> 不支持外键
>
> 支持表锁、不支持行锁
>
> 访问速度快
>
> 文件：xxx.sdi：存储表结构信息(存放的数据为json格式)、xxx.myd：存储数据、xxx.myi：存储索引

3、memory:

> 表数据存放在内存中(前两个存放在硬盘中)
>
> 访问速度快
>
> 支持哈希索引
>
> 文件：xxx.sdi：存储表结构信息

![This is a picture](E:\工具\typora\笔记\DataBase\datas\存储引擎特点.png)
