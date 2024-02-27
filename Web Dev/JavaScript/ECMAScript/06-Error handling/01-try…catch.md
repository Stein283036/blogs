# JavaScript try…catch

## Introduction to JavaScript try…catch statement

以下示例尝试调用不存在的 add() 函数：

```js
let result = add(10, 20);
console.log(result);

console.log('Bye');
```

JavaScript 引擎发出以下错误：

```js
Uncaught ReferenceError: add is not defined
```

错误消息指出 add 没有被定义，错误类型为 ReferenceError。

当 JavaScript 引擎遇到错误时，它会发出该错误并立即终止整个脚本的执行。在上面的示例中，代码执行在第一行停止。

要处理错误并继续执行。为此，可以使用带有以下语法的 try...catch 语句：

```js
try {
  // code may cause error
} catch(error){
  // code to handle error
}
```

如果 try 块中发生错误，JavaScript 引擎会立即执行 catch 块中的代码。此外，JavaScript 引擎将错误对象传递给了 catch 块的参数，其中包含有关错误的详细信息。

基本上，error 对象至少有两个属性：

- `name` specifies the error name.
- `message` explains the error in detail.

如果 try 块中没有发生错误，JavaScript 引擎将忽略 catch 块。

> Note that web browsers may add more properties to the `error` object. For example, Firefox adds `filename`, `lineNumber`, and `stack` properties to the `error` object.

最好只将可能导致异常的代码放在 try 块中。

以下流程图说明了 try...catch 语句的工作原理：

<img src="https://www.javascripttutorial.net/wp-content/uploads/2022/01/JavaScript-try-catch-1.svg" alt="img" style="zoom:80%;" />

## JavaScript try…catch statement examples

以下示例使用 try...catch 语句来处理错误：

```js
try {
  let result = add(10, 20);
  console.log(result);
} catch (e) {
  console.log({ name: e.name, message: e.message });
}
console.log('Bye');
```

输出：

```js
{ name: 'ReferenceError', message: 'add is not defined' }
Bye
```

### Ignoring the catch block

```js
const add = (x, y) => x + y;

try {
  let result = add(10, 20);
  console.log(result);
} catch (e) {
  console.log({ name: e.name, message: e.message });
}
console.log('Bye');
```

输出：

```js
30
Bye
```

## The exception identifier

当 try 块中发生异常时，catch 块中的异常变量（e）存储异常对象。

如果不需要该异常对象，则可以省略它：

```js
try {
  //...
} catch {
  //...
}
```

```js
const isValidJSON = (str) => {
  try {
    JSON.parse(str);
    return true;
  } catch {
    return false;
  }
};

const valid = isValidJson(`{"name": "stein", "age": 23}`)
console.log(valid) // true
```
