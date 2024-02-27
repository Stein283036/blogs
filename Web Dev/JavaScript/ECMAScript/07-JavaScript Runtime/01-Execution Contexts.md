# JavaScript Execution Context

## Introduction to the JavaScript execution context

全局上下文中的变量包括全局对象（如 `window` 对象）、全局函数、全局变量等。这些变量会被存储在堆内存中，并且在整个程序的执行过程中都可以访问到。

有以下代码：

```js
let x = 10;

function timesTen(a){
    return a * 10;
}

let y = timesTen(x);

console.log(y); // 100
```

JavaScript 在幕后做了很多事情。重点关注执行上下文。

当 JavaScript 引擎执行 JavaScript 代码时，它会创建执行上下文。

每个执行上下文都有**两个阶段：创建阶段和执行阶段**。

## The creation phase

When the JavaScript engine executes a script for the first time, it creates the global execution context. During this phase, the JavaScript engine performs the following tasks:

- Create the global object i.e., window in the web browser or global in Node.js.
- Create the this object and bind it to the global object.
- Set up a memory heap for storing variables and function references.
- Store the function declarations in the memory heap and variables within the global execution context with the initial values as undefined.

当 JavaScript 引擎执行上面的代码示例时，它在创建阶段执行以下操作：

- 首先，将变量 x 和 y 以及函数声明 timesTen() 存储在全局执行上下文中。
- 其次，将变量 x 和 y 初始化为 undefined。

创建阶段之后，全局执行上下文进入执行阶段。

## The execution phase

在执行阶段，JavaScript 引擎逐行执行代码，为变量赋值，并执行函数调用。

![javascript execution context - global execution context in execution phase](https://www.javascripttutorial.net/wp-content/uploads/2019/12/javascript-execution-context-global-execution-context-in-execution-phase.png)

**对于每个函数调用，JavaScript 引擎都会创建一个新的函数执行上下文（function execution context）。**

函数执行上下文与全局执行上下文类似。但 JavaScript 引擎不是创建全局对象，而是创建 arguments 对象，该对象是对函数所有形参的引用：

<img src="https://www.javascripttutorial.net/wp-content/uploads/2019/12/javascript-execution-context-function-execution-context-in-creation-phase.png" alt="javascript execution context - function execution context in creation phase" style="zoom:80%;" />

在示例中，函数执行上下文创建引用传递到函数中的所有参数的 arguments 对象，将 this 值设置为全局对象（严格模式下 this 值是 undefined），并将 a 参数初始化为 undefined。

在函数执行上下文的执行阶段，JavaScript 引擎将10 赋值给参数 a，并将结果（100）返回给全局执行上下文：

![javascript execution context - function execution context in execution phase](https://www.javascripttutorial.net/wp-content/uploads/2019/12/javascript-execution-context-function-execution-context-in-execution-phase.png)

为了跟踪所有执行上下文，包括全局执行上下文和函数执行上下文，JavaScript 引擎使用调用堆栈（call stack）。