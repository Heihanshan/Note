# SQL-DCL

## 1、用户管理

```mysql
-- 1、查询用户
use mysql;
select * from user;
-- 2、创建用户
create user '用户名'@'主机名' identified by '密码';-- @左右不用空格,主机名为%时代表任意主机(代表任意主机都能访问该MySQL服务器)
-- 3、修改用户密码
alter user '用户名'@'主机名' identified with mysql_native_password by '新密码';
-- 4、删除用户
drop user '用户名'@'主机名';
```

## 2、权限控制

1、权限种类

> 所有权限：all,all privileges
>
> 查询数据：select
>
> 插入数据：insert
>
> 修改数据：update
>
> 删除数据：delete
>
> 修改表：alter
>
> 删除权限：drop
>
> 创建权限：create

```mysql
-- 1、查询用户权限
show grants for '用户名'@'主机名';
-- 2、授予权限
grant 权限列表 on 数据库名.表名 to '用户名'@'主机名';-- 若给所有数据库所有表授予权限则写... on *.* to ...
-- 例：grant all on itcast.* to 'heima'@'%';
-- 3、撤销权限
revoke 权限列表 on 数据库名.表名 from '用户名'@'主机名';
```



