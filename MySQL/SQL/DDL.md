# DDL-Data Definition Language

## 概述

DDL 是数据定义语言，用于定义数据库和表结构，包括创建、修改和删除数据库（表）对象。

## 数据库

### 查询所有数据库

```mysql
SHOW DATABASES;
```

### 创建数据库

```mysql
CREATE DATABASE database_name CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
# utf8mb4 是字符集的名称，它支持更广泛的 Unicode 字符集，通常用于支持各种语言和符号。
# utf8mb4_unicode_ci 是排序规则（Collation），它定义了字符的比较和排序方式，utf8mb4_unicode_ci 通常用于提供不区分大小写的排序。
```

```mysql
CREATE DATABASE IF NOT EXISTS database_name;
# 在创建数据库之前先判断是否存在已有的数据库
```

### 删除数据库

```mysql
DROP DATABASE database_name;
DROP DATABASE IF EXISTS database_name; # 删除前判断数据库是否存在
```

### 数据库查看和使用

```mysql
USE database_name; # 使用数据库
SELECT DATABASE(); # 查看当前使用的数据库
```

## 数据表

### 查询数据库的所有表

```mysql
SHOW TABLES;
```

### 查看表结构

```mysql
DESC table_name;
```

### 创建数据表

```mysql
CREATE TABLE `table_name` (
    column1 datatype constraint,
    column2 datatype constraint,
);
```

#### 约束

- 主键约束 `PRIMARY KEY`

- 非空约束 `NOT NULL`

- 唯一约束 `UNIQUE`

- 检查约束 `CHECK`

  > MySQL 的 SQL 语句可以使用 `CHECK` 约束，但这个约束不会有任何作用。

- 默认约束 `DEFAULT`

- 外键约束 `FOREIGN KEY`

  **建表时添加外键约束**

  ```mysql
  CREATE TABLE orders (
      order_id INT PRIMARY KEY,
      product_id INT,
      customer_id INT,
      order_date DATE,
      -- Other columns...
      CONSTRAINT fk_orders_products FOREIGN KEY (product_id) REFERENCES products(product_id),
      CONSTRAINT fk_orders_customers FOREIGN KEY (customer_id) REFERENCES customers(customer_id)
  );
  ```

  **建完表之后添加外键约束**

  ```mysql
  ALTER TABLE your_table_name
  ADD CONSTRAINT constraint_name # 例如 fk_emp_dept
  FOREIGN KEY (your_column)
  REFERENCES referenced_table(referenced_column)
  ON DELETE action
  ON UPDATE action;
  # ON DELETE action 定义了在引用表中删除行时采取的动作，可选值包括 CASCADE、SET NULL、SET DEFAULT 或 RESTRICT。
  # ON UPDATE action 定义了在引用表中更新行时采取的动作，可选值也包括 CASCADE、SET NULL、SET DEFAULT 或 RESTRICT。
  ```

  **删除外键约束**

  ```mysql
  ALTER TABLE talbe_name
  DROP FOREIGN KEY constraint_name;
  ```

### 删除数据表

```mysql
DROP TABLE `table_name`;
DROP TABLE IF EXISTS table_name; # 删除前判断是否存在
```

### 修改数据表

#### 修改表名称

```mysql
alter table `old_table_name` rename to `new_table_name`;
```

#### 添加列

```mysql
ALTER TABLE `table_name` ADD COLUMN `column_name` ;
```

#### 修改列

```mysql
alter table `table_name` modify `column_name` datatype; # 修改数据类型
```

```mysql
alter table `table_name` change `old_column_name` `new_column_name` datatype; # 修改列名和数据类型
```

#### 删除列

```mysql
alter table `table_name` drop `column_name`;
```

















