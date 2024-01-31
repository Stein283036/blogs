# DCL-Data Control Language

## 概述

DCL 是数据控制语言，用于授予或撤销访问数据库的权限。

## 授予访问数据库的权限

```mysql
GRANT permission ON object TO user;
# permission 表示授予的权限，比如 SELECT, INSERT, UPDATE, DELETE, ALL PRIVILEGES 等。
# object 是授予权限的对象，可以是数据库、表或列等。
# user 是被授权用户的用户名。
```

```mysql
GRANT SELECT ON exampledb.* TO 'john'@'localhost';
# 授予用户 john 对数据库 exampledb 中所有表的查询权限
```

```mysql
# 授予所有权限
GRANT ALL PRIVILEGES
ON object
TO user;
```

```mysql
GRANT ALL PRIVILEGES ON exampledb.* TO 'admin'@'localhost';
# 授予用户 admin 对数据库 exampledb 中的所有表的所有权限
```

## 撤销访问数据库的权限

```mysql
REVOKE permission ON object FROM user;
# permission 和 object 的含义与 GRANT 语句相同。
# user 是要撤销权限的用户。
```

```mysql
REVOKE SELECT ON exampledb.* FROM 'john'@'localhost';
# 撤销用户 john 对数据库 exampledb 中所有表的查询权限
```

