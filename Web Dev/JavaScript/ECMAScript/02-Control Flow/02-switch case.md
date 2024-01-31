# switch case

## Introduction to the JavaScript switch case statement

switch 语句计算表达式，将其结果与 case 值进行比较，并执行与匹配的 case 值关联的语句。

**switch 语句使用严格比较 (===) 将表达式与 case 值进行比较。**

```js
switch (expression) {
    case value1:
        statement1;
        break;
    case value2:
        statement2;
        break;
    case value3:
        statement3;
        break;
    default:
        statement;
}
```

在实践中，经常使用 switch 语句来替换复杂的 if...else...if 语句，以使代码更具可读性。

从技术上讲，switch 语句相当于以下 if...else...if 语句：

```js
if (expression === value1) {
  statement1;
} else if (expression === value2) {
  statement2;
} else if (expression === value3) {
  statement3;
} else {
  statement;
}
```







