# JavaScript Variable Scopes

## What is variable scope

作用域决定变量的可见性和可访问性。 JavaScript 具有三个作用域：

- The global scope
- Local (Function) scope
- Block scope (started from ES6)

## The global scope

当 JavaScript 引擎执行脚本时，它会创建一个全局执行上下文。

> 在 JavaScript 中，全局执行上下文中的变量存储在堆内存中。堆内存是用于存储动态分配的对象和变量的一种内存区域，它的大小不固定，并且可以动态地分配和释放内存。

此外，它还将在函数外部声明的变量分配给全局执行上下文。这些变量在全局范围内。它们也称为全局变量。

```js
var message = 'Hi';
```

The variable `message` is global-scoped. It can be accessible everywhere in the script.

![JavaScript Global Variables](https://www.javascripttutorial.net/wp-content/uploads/2019/12/JavaScript-Global-Variables.png)

## Local scope

在函数内声明的变量是该函数的局部变量。它们被称为局部变量。

```js
var message = 'Hi';

function say() {
    var message = 'Hello';
    console.log(message);
}

say();
console.log(message);
```

当 JavaScript 引擎执行 say() 函数时，它会创建一个函数执行上下文。 say() 函数内部声明的变量 message 绑定到该函数的函数执行上下文，而不是全局执行上下文。

<img src="https://www.javascripttutorial.net/wp-content/uploads/2019/12/JavaScript-Local-Variables.png" alt="JavaScript Local Variables" style="zoom:80%;" />

## Scope chain

```js
var message = 'Hi';

function say() {
    console.log(message);
}

say(); // Hi
```

在 say() 函数内引用变量 message。 JavaScript 在幕后执行以下操作：

- 在 say() 函数的当前上下文（函数执行上下文）中查找变量 message，没有找到。
- 在外部执行上下文（即全局执行上下文）中找到变量 message。它找到变量 message。

JavaScript 解析变量的方式是在当前作用域中查找变量，如果找不到该变量，则会向上查找外部作用域，这称为作用域链。

<img src="https://www.javascripttutorial.net/wp-content/uploads/2019/12/JavaScript-Scope-Chain.png" alt="JavaScript Scope Chain" style="zoom:80%;" />

### More scope chain example

```js
var y = 20;

function bar() {
    var y = 200;

    function baz() {  
        console.log(y);
    }

    baz();
}

bar(); // 200
```

在这个例子中：

- JS 引擎现在 baz 的函数执行上下文中查找变量 y，没有找到，于是向上一次执行上下文即 bar 的函数执行上下文查找。
- 然后，JavaScript 引擎在 bar() 函数执行上下文中找到变量 y，因此停止搜索，不会查找全局执行上下文中的 y 变量。

## Global variable leaks: the weird part of JavaScript

```js
function getCounter() {
    counter = 10;
    return counter;
}

console.log(getCounter()); // 10
console.log(window.counter) // 10
```

在此示例中，将 10 分配给不带 var、let 或 const 关键字的 counter 变量，然后返回它。

在函数外部，调用了 getCounter() 函数并在控制台中显示结果。

这个问题被称为全局变量泄漏。

在底层，JavaScript 引擎首先在 getCounter() 函数的 local scope 内查找 counter 变量。由于没有 var、let 或 const 关键字，因此 counter 变量在 local scope 中不可用。它尚未被创建。

然后，JavaScript 引擎沿着作用域链并在全局作用域中查找 counter 变量。全局作用域也没有 counter 变量，因此 JavaScript 引擎在全局作用域中创建 counter 变量。

要修复这种“奇怪”的行为，可以在脚本顶部或函数顶部使用 “use strict”：

```js
'use strict'

function getCounter() {
    counter = 10;
    return counter;
}

console.log(getCounter()); // ReferenceError: counter is not defined
```

## Block scope

ES6 提供了 let 和 const 关键字，允许在 block scope 中声明变量。

Generally, whenever you see curly brackets `{}`, it is a block. It can be the area within the `if`, `else`, `switch` conditions or `for`, `do while`, and `while` loops.

```js
function say(message) {
    if(!message) {
        let greeting = 'Hello'; // block scope
        console.log(greeting);
    }
    // say it again ?
    console.log(greeting); // uncaught ReferenceError: greeting is not defined
}

say();
```