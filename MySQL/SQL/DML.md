# DML-Data Manipulation Language

## 概述

DML 是数据操纵语言，用于对数据库中的数据进行操作，包括插入、更新和删除数据。

## 更新

```mysql
UPDATE table_name SET column1 = value1, column2 = value2, ... WHERE condition;
```

## 插入

```mysql
INSERT INTO table_name (column1, column2, ...) VALUES (value1, value2, ...); # 向指定列插入多行记录
```

```mysql
INSERT INTO table_name VALUES(value1, value2, ...) # 向所有的列插入多行记录
```

## 删除

```mysql
DELETE FROM table_name WHERE condition;
```





