# TCL-Transaction Control Language

## 概述

TCl 是事务控制语言，用于管理事务，包括创建保存点、提交和回滚。

## 事务管理

```mysql
BEGIN; -- 开始事务
-- 执行一些 SQL 操作
SAVEPOINT my_savepoint; -- 创建保存点
-- 执行更多 SQL 操作
ROLLBACK TO my_savepoint; -- 回滚到保存点
COMMIT; -- 提交事务
```

```mysql
# 查询事务的默认提交方式
# MySQL 事务默认自动提交
select @@autocommit; # 1 是自动提交，0 是手动提交
```

```mysql
# 修改事务的提交方式
set @@autocommit = 0;
```

