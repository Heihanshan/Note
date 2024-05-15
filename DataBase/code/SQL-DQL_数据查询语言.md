# DQL

## 一、基本查询

```mysql
-- 查询多个字段
select 字段1,字段2,字段3,…… from 表名;
-- 查询所有字段
select *from 表名;
-- 设置别名(只是执行后能看到别名，实际的表还是原来的名字)
select 字段1[as 别名1],字段2[as 别名2]…… from 表名;  -- as可以省略
-- 去除重复记录
select distinct 字段列表 from tableName;
```

## 二、条件查询

> 大于：>、大于等于：>=、小于：<、小于等于：<=、等于：=
>
> 不等于:<>、!=
>
> 在某个范围之内(含最大最小值):between 最小值 and 最大值
>
> in内的值满足其一即可查询：In(…)
>
> 模糊匹配：like _(匹配单个字符)，%(匹配任意个字符)
>
> 为空：is NULL、不为空:is not NULL
>
> 并：and或&&
>
> 或：or或||
>
> 非：not、!

```mysql
-- 1、语法
select 字段列表 from 表名 where 条件列表
-- 例：
select 字段 from 表名 where age>=20 and age<=40;
select 字段 from 表名 where age between 20 and 40;
select 字段 from 表名 where age=18 or age=20 or age=40;
-- 查询年龄为18或20或40
select 字段 from 表名 where age in(18,20,40);
-- 查询所有姓名为两个字的人
select 字段 from 表名 where name like '__';
-- 查询所有名字最后一个字为浩的人(前面多少个字符无所谓)
select 字段 from 表名 where name like '%浩'
```

## 三、聚合函数

1、使用：将一列数据作为整体进行纵向计算(NULL不参与计算)

> count :统计数量
>
> max:最大值
>
> min:最小值
>
> avg:平均值
>
> sum:求和

```mysql
-- 求整张表的列数
select count(*) from 表名;
-- 求某字段列数
select count(字段名) from 表名
-- 求某字段平均数
select avg(字段名) from 表名;
-- 求某字段最大值
select max(字段名) from 表名;
-- 求某字段的和
select sum(age) from 表名;
-- 若加上条件
select sum(age) from 表名 条件列表;
select sum(age) from 表名 where age>=20 and age<=40;
```

## 四、分组查询

 ```mysql
 -- 语法(where在分组前过滤，having对分组后的数据过滤，where不能对聚合函数判断，having可以.分组指的是分组字段名中所有相同字段值的为一组)
 select 字段列表 from 表名 [where 条件] group by 分组字段名 [having 分组后过滤条件];
 -- 例
 -- 1、查询grade 表中总分大于400 分的学生的学号和总分，查询结果按总分的升序显示。
 SELECT 学号, SUM(分数) AS 总分 FROM grade GROUP BY 学号 HAVING SUM(分数) > 400 ORDER BY 总分 ASC;
 -- 2、根据性别分组，统计男女员工数量
 select gender,count(gender) from emp group by gender;
 -- 3、查询年龄小于45的员工，并根据工作地点分组，获取员工数量大于3的工作地址
 select workaddress,count(workaddress) from emp where age<45 group by workaddress having count(workaddress)>=3;
 ```

执行顺序：where>聚合函数>having

## 五、排序查询

```mysql
-- 语法
select 字段列表 from 表名 order by 字段1 排序方式1,字段2 排序方式2,...;
-- 排序方式
1、asc：升序（默认值）
2、desc：降序
-- 例
查询学生的学号、姓名、性别、出生日期及家庭住址，查询结果先按照性别的由小到大排序，性别相同的再按学号由大到小排序
SELECT 学号,姓名,性别,出生日期,家庭住址 FROM student_info ORDER BY 性别 ASC,学号 DESC;
```

## 六、分页查询

```mysql
-- 语法
select 字段列表 from 表名 limit 起始索引,查询记录数;
-- 起始索引从0开始，起始索引=(查询页码-1)*每页显示记录数(由自己在查询记录数设定)
-- 如果查询第一页数据，起始索引可以省略

-- 例
-- 查询第一页数据每页展示10条记录
select 字段名 from 表名 limit 0,10; 或 select 字段名 from 表名 limit 10;
-- 查询第二页数据每页展示10条记录
select 字段名 from 表名 limit 10,10;-- 注意前一个是10不是2，公式为(2-1)*10=10
```

## 七、执行顺序

1、编写顺序：

> select 字段列表
>
> from 表名列表 
>
> where  条件列表
>
> group by 分组字段列表 
>
> having 分组后条件列表
>
> order by 排序字段列表 
>
> limit 分页参数

2、执行顺序：

> from 表名列表
>
> where  条件列表
>
> group by 分组字段列表
>
> having 分组后条件列表
>
> select 字段列表 
>
> order by 排序字段列表
>
> limit 分页参数
