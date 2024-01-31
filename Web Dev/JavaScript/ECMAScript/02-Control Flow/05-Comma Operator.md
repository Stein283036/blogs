# Comma Operator

## Introduction to the JavaScript comma operator

JavaScript 使用逗号 (,) 来表示逗号运算符。逗号运算符接受多个表达式，从左到右计算它们，并返回右侧表达式的值。

以下是逗号运算符的语法：

```js
leftExpression, ..., rightExpression
```

```js
let result = (10, 10 + 20);
console.log(result); // 30
```

```js
let x = 10;
let y = (x++, x + 1);

console.log(x, y); // 11 12
```

在实践中，可能希望在 for 循环中使用逗号运算符，以便每次通过循环更新多个变量。

以下示例在 for 循环中使用逗号运算符将包含九个元素的数组显示为 3 行 3 列的矩阵：

```js
let board = [1, 2, 3, 4, 5, 6, 7, 8, 9];

let s = '';
for (let i = 0, j = 1; i < board.length; i++, j++) {
  s += board[i] + ' ';
  if (j % 3 == 0) {
    console.log(s);
    s = '';
  }
}
// 输出
1 2 3
4 5 6
7 8 9
```









