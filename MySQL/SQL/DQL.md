# DQL-Data Query Language

## 概述

DQL 是数据查询语言，用于查询数据库中的数据。

## 基础查询

```mysql
SELECT * # 查询所有列
FROM table_name;
```

```mysql
SELECT column1, column2 # 查询特定列
FROM table_name;
```

```mysql
SELECT column1 c1, column2 as c2 # 给指定的列起别名
FROM table_name;
```

```mysql
SELECT DISTINCT column1, column2 # 去除重复记录
FROM table_name;
```

## 条件查询

### 比较条件

- `>`
- `<`
- `>=`
- `<=`
- `<>` `!=`

### 范围条件

- `BETWEEN AND`
- `IN()`

### 模糊条件

- `LIKE regex` _单个任意字符 %多个任意字符

### 存在条件

- `IS NULL`
- `IS NOT NULL`

### 逻辑条件

- `AND` `&&`
- `OR` `||`
- `NOT` `!`

```mysql
SELECT *
FROM table_name
WHERE condition;
```

## 分组查询

## 排序查询

## 分页查询

## 多表查询

## 完整查询

```mysql
SELECT columns
FROM table_name
WHERE condition # 分组前的条件过滤
GROUP BY column
HAVING condition # 分组后的条件过滤
ORDER BY column asc(desc)
LIMIT offset, row_count;
# offset 是起始行的偏移量，表示从结果集中的第几行开始返回数据（从 0 开始计数）。
# row_count 是要返回的行数。
```



