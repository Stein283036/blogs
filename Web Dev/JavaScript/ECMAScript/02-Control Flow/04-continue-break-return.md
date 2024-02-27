# continue-break-return

## JavaScript break

### The label statement

在 JavaScript 中，可以为语句添加标签以供以后使用。这是标签语句的语法：

```js
label: statement;
```

```js
outer: for (let i = 0; i < 5; i++) {
    console.log(i);
}
```

定义标签后，可以在 break 或 continue 语句中引用它。

### Introduction to JavaScript break statement

Break 语句提前终止循环，例如 for、do...while 和 while 循环、switch 或标签语句。下面是break语句的语法：

```js
break [label];
```

在此语法中，如果在循环或 switch 中使用break语句，则标签是可选的。但是，如果将break语句与标签语句一起使用，则需要指定它。

## JavaScript continue

### Introduction to the JavaScript continue statement

continue 语句终止循环（例如 for、while 和 do…while 循环）的当前迭代中的语句的执行，并立即继续下一次迭代。

continue 语句的语法：

```js
continue [label];
```

### Using the continue statement with a label example

```js
outer: for (let i = 1; i < 4; i++) {
  for (let j = 1; j < 4; j++) {
    if (i + j == 3) continue outer;
    console.log(i, j);
  }
}
// 输出
1 1
3 1
3 2
3 3
```
