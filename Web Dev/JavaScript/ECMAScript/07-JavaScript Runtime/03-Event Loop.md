# JavaScript Event Loop

## JavaScript single-threaded model

JavaScript 是一种单线程编程语言。这意味着 JavaScript 在单个时间点只能做一件事。

JavaScript 引擎从文件顶部开始执行脚本，然后向下执行。它创建执行上下文，并在执行阶段将函数压入调用堆栈或从调用堆栈弹出。

如果某个函数需要很长时间执行，则在该函数执行期间无法与 Web 浏览器交互，因为页面会挂起。

需要很长时间才能完成的函数称为阻塞函数。从技术上讲，阻塞函数会阻止网页上的所有交互，例如鼠标点击。

阻塞函数的一个示例是从远程服务器调用 API 的函数。

以下示例使用大循环来模拟阻塞函数：

```js
function task(message) {
    // emulate time consuming task
    let n = 10000000000;
    while (n > 0){
        n--;
    }
    console.log(message);
}

console.log('Start script...');
task('Call an API');
console.log('Done!');
```

在此示例中，在 task() 函数内有一个很大的 while 循环来模拟耗时的任务。 task() 函数是一个阻塞函数。

该脚本挂起几秒钟（取决于计算机的速度）并输出：

```js
Start script...
Call an API
Done!
```

为了执行脚本，JavaScript 引擎将第一个调用 console.log() 放在调用堆栈的顶部并执行它。然后，它将 task() 函数放置在调用堆栈的顶部并执行该函数。

然而，完成 task() 函数需要一段时间。因此，过一会才会看到 Call an API 消息。task() 函数完成后，JavaScript 引擎将其从调用堆栈中弹出。

Finally, the JavaScript engine places the last call to the `console.log('Done!')` function and executes it, which will be very fast.

<img src="https://www.javascripttutorial.net/wp-content/uploads/2019/12/javascript-event-loop-callstack.png" alt="javascript event loop - callstack" style="zoom:80%;" />

## Callbacks to the rescue

为了防止阻塞函数阻塞其他活动，通常将其放入回调函数中以便稍后执行。例如：

```js
console.log('Start script...');

setTimeout(() => {
    task('Download a file.');
}, 1000);

console.log('Done!');
```

In this example, you’ll see the message `'Start script...'` and `'Done!'` immediately. And after that, you’ll see the message `'Download a file'`.

As mentioned earlier, the JavaScript engine can do only one thing at a time. However, it’s more precise to say that the JavaScript **runtime** can do one thing at a time.

Web 浏览器还有其他组件，而不仅仅是 JavaScript 引擎。

当调用 setTimeout() 函数、进行 fetch request 或单击按钮时，Web 浏览器可以并发且异步地执行这些活动。

The setTimeout(), fetch requests and DOM events are parts of the Web APIs of the web browser.

在示例中，当调用 setTimeout() 函数时，JavaScript 引擎将其放置在 call stack上，并且 Web API 创建一个在 1 秒后到期的计时器。

<img src="https://www.javascripttutorial.net/wp-content/uploads/2019/12/javascript-event-loop-step-1.png" alt="javascript event loop - step 1" style="zoom:80%;" />

然后 JavaScript 引擎将 task() 函数放入一个称为回调队列（callback queue）或任务队列的队列中：

<img src="https://www.javascripttutorial.net/wp-content/uploads/2019/12/javascript-event-loop-step-2.png" alt="javascript event loop - step 2" style="zoom:80%;" />

事件循环（event loop）是一个持续运行的进程，它监视回调队列和调用堆栈。

如果调用堆栈不为空，则 event loop 将等待直至其为空，并将回调队列中的下一个函数放入调用堆栈。如果回调队列为空，则不会发生任何事情：

<img src="https://www.javascripttutorial.net/wp-content/uploads/2019/12/javascript-event-loop-step-3.png" alt="javascript event loop - step 3" style="zoom:80%;" />

看另一个例子：

```js
console.log('Hi!');

setTimeout(() => {
    console.log('Execute immediately.');
}, 0);

console.log('Bye!');
```

In this example, the timeout is 0 seconds, so the message `'Execute immediately.'` should appear before the message `'Bye!'`. However, it doesn’t work like that.

The JavaScript engine places the following function call on the callback queue and executes it when the call stack is empty. In other words, the JavaScript engine executes it after the `console.log('Bye!')`.

```js
console.log('Execute immediately.');
```

输出：

```js
Hi!
Bye!
Execute immediately.
```

The following picture illustrates JavaScript runtime, Web API, Call stack, and Event loop:

<img src="https://www.javascripttutorial.net/wp-content/uploads/2019/12/javascript-event-loop.png" alt="javascript event loop" style="zoom:80%;" />