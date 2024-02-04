# JavaScript Call Stack

## Introduction to JavaScript Call Stack

调用堆栈是 JavaScript 引擎跟踪其在调用多个函数的代码中的位置的一种方式。它包含有关当前正在运行哪些函数以及从该函数内调用哪些函数的信息......

此外，JavaScript 引擎使用调用堆栈来管理执行上下文：

- The global execution context
- Function execution contexts

调用堆栈基于后进先出 (LIFO) 原则工作。

当您执行脚本时，JavaScript 引擎会创建一个全局执行上下文并将其推送到调用堆栈的顶部。

每当调用函数时，JavaScript 引擎都会为该函数创建一个函数执行上下文，将其推送到调用堆栈顶部，然后开始执行该函数。

如果一个函数调用另一个函数，JavaScript 引擎会为被调用的函数创建一个新的函数执行上下文，并将其推送到调用堆栈的顶部。

当当前函数完成时，JavaScript 引擎将其从调用堆栈中弹出，并从中断处恢复执行。

当调用堆栈为空时，脚本将停止。

## JavaScript call stack example

```js
function add(a, b) {
    return a + b;
}

function average(a, b) {
    return add(a, b) / 2;
}

let x = average(10, 20);
```

当 JavaScript 引擎执行此脚本时，它将全局执行上下文（由 main() 或 global() 函数表示）放置在调用堆栈上。

![JavaScript Call Stack - main](https://www.javascripttutorial.net/wp-content/uploads/2019/12/JavaScript-Call-Stack-main.png)

全局执行上下文进入创建阶段并移动到执行阶段。

JavaScript 引擎执行对average(10, 20) 函数的调用，并为average() 函数创建一个函数执行上下文，并将其推送到调用堆栈的顶部：

![JavaScript Call Stack - step 2](https://www.javascripttutorial.net/wp-content/uploads/2019/12/JavaScript-Call-Stack-step-2.png)

JavaScript 引擎开始执行average()，因为average() 函数位于调用堆栈的顶部。

Average() 函数调用 add() 函数。此时，JavaScript 引擎为 add() 函数创建另一个函数执行上下文，并将其放置在调用堆栈的顶部：

![JavaScript Call Stack - step 3](https://www.javascripttutorial.net/wp-content/uploads/2019/12/JavaScript-Call-Stack-step-3.png)

JavaScript 引擎执行 add() 函数并将其从调用堆栈中弹出：

![JavaScript Call Stack - step 4](https://www.javascripttutorial.net/wp-content/uploads/2019/12/JavaScript-Call-Stack-step-4.png)

此时，average()函数位于调用堆栈的顶部，JavaScript引擎执行并将其从调用堆栈中弹出。

![JavaScript Call Stack - step 5](https://www.javascripttutorial.net/wp-content/uploads/2019/12/JavaScript-Call-Stack-step-5.png)

现在，调用堆栈为空，因此脚本停止执行：

![JavaScript Call Stack - empty stack](https://www.javascripttutorial.net/wp-content/uploads/2019/12/JavaScript-Call-Stack-empty-stack.png)

## Stack Overflow

call stack 具有固定大小，具体取决于主机环境（Web 浏览器或 Node.js）的实现。

如果执行上下文的数量超过堆栈的大小，就会发生堆栈溢出错误。

例如，当执行没有退出条件的递归函数时，JavaScript引擎将发出堆栈溢出错误：

```js
function fn() {
    fn();
}

fn(); // RangeError: Maximum call stack size exceeded
```

## Asynchronous JavaScript

JavaScript 是一种单线程编程语言。这意味着 JavaScript 引擎只有一个调用堆栈。因此，它一次只能做一件事。

执行脚本时，JavaScript 引擎从上到下逐行执行代码。换句话说，它是同步的。

异步意味着 JavaScript 引擎可以在等待另一个任务完成的同时执行其他任务。例如，JavaScript 引擎可以：

- Request for data from a remote server.
- Display a spinner
- When the data is available, display it on the webpage.

实现上述异步，JavaScript 引擎使用事件循环（event loop）。