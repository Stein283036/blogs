# JavaScript setTimeout

## Introduction to JavaScript `setTimeout()`

The `setTimeout()` is a method of the `window` object. The `setTimeout()` sets a timer and executes a callback function after the timer expires.

```js
setTimeout(handler: TimerHandler, timeout?: number, ...arguments: any[]): number
```

`timeout` is the time in milliseconds that the timer should wait before executing the callback function. If you omit it, the `timeout` defaults to 0.

The `setTimeout()` returns a `timeoutID` which is a positive integer identifying the timer created as a result of calling the method.

The `timeoutID` can be used to cancel timeout by passing it to the `clearTimeout()` method.

## JavaScript `setTimeout()` example

### HTML

```html
<p>JavaScript setTimeout Demo</p>
<button onclick="showAlert();">Show</button>
<button onclick="cancelAlert();">Cancel</button>
```

### JavaScript

```javascript
var timeoutID;

function showAlert() {
    timeoutID = setTimeout(alert, 3000, 'setTimeout Demo!');
}

function clearAlert() {
    clearTimeout(timeoutID);
}
```

## How JavaScript `setTimeout()` works

JavaScript is single-threaded therefore it can only do one task at a time. It means that it can only carry a single task a given time.Besides the JavaScript engine, the web browser has other components such as Event Loop, Call Stack, and Web API.

When you call the `setTimeout()`, the JavaScript engine creates a new function execution context and places it on the call stack.

The `setTimeout()` executes and creates a timer in the Web APIs component of the web browser. When the timer expires, the callback function that was passed in the `setTimeout()` is placed to the callback queue.

The event loop monitors both the call stack and the callback queue. It removes the callback function from the callback queue and places it to call stack when the call stack is empty.

Once the callback function is on the call stack, it is executed.

```js
function task() {
    console.log('setTimeout Demo!')
}

setTimeout(task, 3000);
```

First, the `setTimeout()` is placed on the call stack. It creates a timer on Web API.

![javascript setTimeout step 1](D:\2024年\blogs\Web Dev\JavaScript\BOM\01-Window\assets\javascript-setTimeout-step-1.png)

Second, after roughly 3 seconds, the timer expires, the `task` is pushed to the callback queue and waited for the next opportunity to execute.

![javascript setTimeout step 2](D:\2024年\blogs\Web Dev\JavaScript\BOM\01-Window\assets\javascript-setTimeout-step-2.png)

Third, because the call stack is empty, the event loop removes the `task()` from the callback queue, places it on the call stack, and executes it:

Fourth, the `console.log()` in the `setTimeout()` executes that creates a new function execution context.

![javascript setTimeout step 4](D:\2024年\blogs\Web Dev\JavaScript\BOM\01-Window\assets\javascript-setTimeout-step-4.png)

Finally, the `console.log()` and `task()` are popped out of the call stack once they are completed.