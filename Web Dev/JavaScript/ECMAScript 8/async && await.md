# JavaScript async/await

## Introduction to JavaScript async / await keywords

过去，为了处理异步操作，经常使用回调函数。但是，当嵌套很多回调函数时，代码会更难维护。最终会遇到一个臭名昭著的问题，即回调地狱。

假设需要按以下顺序执行三个异步操作：

1. Select a user from the database.
2. Get services of the user from an API.
3. Calculate the service cost based on the services from the server. 

以下函数说明了这三个任务。使用 setTimeout() 函数来模拟异步操作。

```js
function getUser(userId, callback) {
    console.log('Get user from the database.');
    setTimeout(() => {
        callback({
            userId: userId,
            username: 'john'
        });
    }, 1000);
}

function getServices(user, callback) {
    console.log(`Get services of  ${user.username} from the API.`);
    setTimeout(() => {
        callback(['Email', 'VPN', 'CDN']);
    }, 2 * 1000);
}

function getServiceCost(services, callback) {
    console.log(`Calculate service costs of ${services}.`);
    setTimeout(() => {
        callback(services.length * 100);
    }, 3 * 1000);
}
```

下图展示了嵌套的回调函数：

```js
getUser(100, (user) => {
    getServices(user, (services) => {
        getServiceCost(services, (cost) => {
            console.log(`The service cost is ${cost}`);
        });
    });
});
```

输出：

```js
Get user from the database.
Get services of  john from the API.
Calculate service costs of Email,VPN,CDN.
The service cost is 300
```

为了避免这种回调地狱问题，ES6 引入了 Promise，可以以更易于管理的方式编写异步代码。

首先，需要在每个函数中返回一个 Promise：

```js
function getUser(userId) {
    return new Promise((resolve, reject) => {
        console.log('Get user from the database.');
        setTimeout(() => {
            resolve({
                userId: userId,
                username: 'john'
            });
        }, 1000);
    })
}

function getServices(user) {
    return new Promise((resolve, reject) => {
        console.log(`Get services of  ${user.username} from the API.`);
        setTimeout(() => {
            resolve(['Email', 'VPN', 'CDN']);
        }, 2 * 1000);
    });
}

function getServiceCost(services) {
    return new Promise((resolve, reject) => {
        console.log(`Calculate service costs of ${services}.`);
        setTimeout(() => {
            resolve(services.length * 100);
        }, 3 * 1000);
    });
}
```

然后，使用 promise chain 链接多个 promise 对象：

```js
getUser(100)
    .then(getServices)
    .then(getServiceCost)
    .then(console.log);
```

ES2017 引入了建立在 Promise 之上的 async/await 关键字，可以编写看起来更像同步代码并且更具可读性的异步代码。从技术上讲，async/await 是 Promise 的语法糖。

如果函数返回 Promise，则可以将await 关键字放在函数调用前面，如下所示：

```js
let result = await f();
```

The `await` will wait for the `Promise` returned from the `f()` to settle. The `await` keyword can be used only inside the `async` functions.

下面定义了一个异步函数，它依次调用三个异步操作：

```js
async function showServiceCost() {
    let user = await getUser(100);
    let services = await getServices(user);
    let cost = await getServiceCost(services);
    console.log(`The service cost is ${cost}`);
}

showServiceCost();
```

## The `async` keyword

async 关键字用来定义处理异步操作的函数。

要定义异步函数，将 async 关键字放在 function 关键字前面，如下所示：

```js
async function sayHi() {
    return 'Hi';
}
```

异步函数通过事件循环（event loop）异步执行。它总是返回一个 Promise。

在此示例中，因为 sayHi() 函数返回一个 Promise，所以可以使用它，如下所示：

```js
sayHi().then(console.log);
```

还可以从 sayHi() 函数显式返回 Promise，如以下代码所示：

```js
async function sayHi() {
    return Promise.resolve('Hi');
}
```

效果是一样的。

除了常规函数之外，还可以在函数表达式中使用 async 关键字：

```js
let sayHi = async function () {
    return 'Hi';
}
```

箭头函数：

```js
let sayHi = async () => 'Hi'; 
```

类的方法：

```js
class Greeter {
    async sayHi() {
        return 'Hi';
    }
}
```

## The `await` keyword

You use the `await` keyword to wait for a `Promise` to settle either in a resolved or rejected state. You can use the `await` keyword **only** inside an `async` function:

```js
async function display() {
    let result = await sayHi();
    console.log(result);
}
```

在此示例中，await 关键字指示 JavaScript 引擎等待 sayHi() 函数完成后再显示消息。

在 async 函数之外使用 await 运算符，将收到错误。

## Error handling

If a promise resolves, the `await promise` returns the result. However, when the promise is rejected, the `await promise` will throw an error as if there were a `throw` statement.

以下代码：

```js
async function getUser(userId) {
     await Promise.reject(new Error('Invalid User Id'));
}
```

等价于：

```js
async function getUser(userId) {
    throw new Error('Invalid User Id');
}
```

可以使用 try...catch 语句捕获错误，就像常规的 throw 语句一样：

```js
async function getUser(userId) {
    try {
       const user = await Promise.reject(new Error('Invalid User Id'));
    } catch(error) {
       console.log(error);
    }
}
```

It’s possible to catch errors caused by one or more `await promise`‘s:

```js
async function showServiceCost() {
    try {
       let user = await getUser(100);
       let services = await getServices(user);
       let cost = await getServiceCost(services);
       console.log(`The service cost is ${cost}`);
    } catch(error) {
       console.log(error);
    }
}
```