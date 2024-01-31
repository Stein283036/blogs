# MySQL Interview

## 存储引擎

MyIASM 和 InnoDB

## SQL 语句优化

- 避免 SELECT *，只查询有限的列
- 使用 LIMIT 子句限制返回的记录
- 为搜索字段添加索引
- 在 WHERE 子句中尽可能的使用 NOT NULL
- 选择正确的存储引擎
- 注意 LIKE 模糊查询的使用，避免使用 %%
- 使用 INSERT 批量插入记录
- 使用 EXPLAIN 查看 SQL 性能
- 尽量不使用子查询
- 建表时尽量给每个字段设置为 NOT NULL，提高查询性能

## 索引

索引是什么，作用。

索引类型。

## 索引失效的情况

- WHERE 子句中使用函数（聚合函数）
- 

## 垂直分库和水平分库

## 数据库事务

## 事务的隔离级别和传播级别

配置文件修改隔离级别

## 数据库三大范式

## 一张自增表里面总共有 7 条数据，删除了最后 2 条数据，重启 MySQL 数据库，又插入了一条数据，此时 id 是多少

表类型如果是 MyISAM ，那 id 就是 8；表类型如果是 InnoDB，那 id 就是 6。

InnoDB 表只会把自增主键的最大 id 记录在内存中，所以重启之后会导致最大 id 丢失。

## 怎么验证 MySQL 的索引是否满足需求？

使用 explain 查看 SQL 是如何执行查询语句的，从而分析你的索引是否满足需求。

explain 语法：explain select * from table where type=1。

## MySQL 的行锁和表锁

## 乐观锁和悲观锁

## MySQL 问题排查

- SHOW PROCESSLIST 查看当前所有连接信息
- EXPLAIN 命令查询 SQL 语句执行
- 开启慢查询日志，查看慢查询的 SQL

