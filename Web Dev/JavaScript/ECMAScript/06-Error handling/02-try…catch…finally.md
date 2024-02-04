# JavaScript try…catch…finally

## Introduction to the JavaScript try…catch…finally statement

有时，无论是否发生异常，都希望执行一个块。在这种情况下，可以使用 try...catch...finally 语句，语法如下：

```js
try {
  // code may cause exceptions
} catch (error) {
  // code to handle exceptions
} finally {
  // code to execute whether exceptions occur or not
}
```

在此语法中，finally 块始终在 try 和 catch 块完成后执行，无论是否发生异常。

下面的流程图说明了 try...catch...finally 的工作原理：

<img src="https://www.javascripttutorial.net/wp-content/uploads/2022/01/javascript-try-catch-finally.svg" alt="JavaScript try...catch...finally" style="zoom:80%;" />

## try…catch…finally and return

无论是否发生异常，finally 块都会执行。此外，无法采取任何措施来阻止它执行，包括使用 return 语句。例如：

```js
function fn() {
  try {
    return 1;
  } catch {
    return 2;
  } finally {
    return 3;
  }
}

console.log(fn()); // 3
```

try...catch...finally 语句中将忽略 try 和 catch 块中的 return 语句。