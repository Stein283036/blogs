# JavaScript Throw Exception

## Introduction to the JavaScript throw statement

throw 语句用于抛出异常。下面是 throw 语句的语法：

```js
throw expression;
```

在此语法中，表达式指定异常的值。通常，将使用 Error 类或其子类的实例。

当遇到 throw 语句时，JavaScript 引擎停止执行并将控制权传递给调用堆栈（call stack）中的第一个 catch 块。如果不存在 catch 块，JavaScript 引擎将终止脚本。

## JavaScript throw exception examples

### Using the JavaScript throw statement to throw an exception

```js
function add(x, y) {
  if (typeof x !== 'number') {
    throw 'The first argument must be a number';
  }
  if (typeof y !== 'number') {
    throw 'The second argument must be a number';
  }

  return x + y;
}

const result = add('a', 10);
console.log(result);
```

该脚本会导致错误，因为第一个实参（“a”）不是数字：

```js
Uncaught The first argument must be a number
```

### Using JavaScript throw statement to throw an instance of the Error class

```js
function add(x, y) {
  if (typeof x !== 'number') {
    throw new Error('The first argument must be a number');
  }
  if (typeof y !== 'number') {
    throw new Error('The second argument must be a number');
  }

  return x + y;
}

try {
  const result = add('a', 10);
  console.log(result);
} catch (e) {
  console.log(e.name, ':', e.message); // Error : The first argument must be a number
}
```

### Using JavaScript throw statement to throw a user-defined exception

有时，需要抛出自定义 Error 而不是内置错误。为此，可以定义一个扩展 Error 类的自定义错误类（custom error class）并抛出该类的新实例。

首先，定义扩展 Error 类的 NumberError：

```js
class NumberError extends Error {
  constructor(value) {
    super(`"${value}" is not a valid number`);
    this.name = 'InvalidNumber';
  }
}
```

在 NumberError 类的 constructor() 中，通过 super 调用 Error 类的构造函数并向其传递一个字符串。此外，将错误名称覆盖为文字字符串 NumberError。如果我们不这样做，NumberError 的 name 将为 Error。

其次，在 add() 函数中使用 NumberError 类：

```js

function add(x, y) {
  if (typeof x !== 'number') {
    throw new NumberError(x);
  }
  if (typeof y !== 'number') {
    throw new NumberError(y);
  }

  return x + y;
}
```

第三，捕获 add() 函数抛出的异常：

```js
try {
  const result = add('a', 10);
  console.log(result);
} catch (e) {
  console.log(e.name, ':', e.message); // InvalidNumber : "a" is not a valid number
}
```





















