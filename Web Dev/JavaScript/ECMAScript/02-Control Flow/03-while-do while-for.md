# while-do while-for

## while loop

JavaScript while 语句创建一个循环，只要条件计算结果为 true，该循环就会执行块中的语句。

```js
while (expression) {
    // statement
}
```

> 请注意，如果想至少执行该语句一次并在每次迭代后检查条件，则应使用 do...while 语句。

## JavaScript do…while Loop

与 while 循环不同，do-while 循环在计算表达式之前总是至少执行一次语句。

由于 do...while 循环在每次迭代后计算表达式，因此通常称为后测试循环。

注意，从 ES6+ 开始，while(表达式) 后面的尾随分号 (;) 是可选的。因此可以使用以下语法：

```js
do {
  statement;
} while(expression)
```

## JavaScript for Loop

for 循环语句创建一个具有三个可选表达式的循环。下面说明了 for 循环语句的语法：

```js
for (initializer; condition; iterator) {
    // statements
}
```

在for循环中，三个表达式是可选的。下面显示了不带任何表达式的 for 循环：

```js
for ( ; ; ) {
   // statements
}
```

### Using the JavaScript for loop without the loop body example

JavaScript 允许 for 语句有一个空语句。在这种情况下，可以在 for 语句之后放置一个分号 (;)。

```js
let sum = 0;
for (let i = 0; i <= 9; i++, sum += i);
console.log(sum); // 55
```
