# Promise Error Handling

假设有一个名为 getUserById() 的函数，它返回一个 Promise：

```js
function getUserById(id) {
    return new Promise((resolve, reject) => {
        resolve({
            id: id,
            username: 'admin'
        });
    });
}
```

## Normal error

首先，更改 getUserById() 函数以在 Promise 之外抛出错误：

```js
function getUserById(id) {
    if (typeof id !== 'number' || id <= 0) {
        throw new Error('Invalid id argument');
    }

    return new Promise((resolve, reject) => {
        resolve({
            id: id,
            username: 'admin'
        });
    });
}
```

其次，使用 then() 和 catch() 方法处理 Promise：

```js
getUserById('a')
    .then(user => console.log(user.username))
    .catch(err => console.log(err));
```

代码抛出一个错误，该错误并没有被 Promise 对象的 catch() 捕获：

```js
Uncaught Error: Invalid id argument
```

当在 Promise 之外引发异常时，必须使用 try/catch 捕获它：

```js
try {
    getUserById('a')
        .then(user => console.log(user.username))
        .catch(err => console.log(`Caught by .catch ${err}`));
} catch (error) {
    console.log(`Caught by try/catch ${error}`); // Caught by try/catch Error: Invalid id argument
}
```

## Errors inside the Promises

更改 getUserById() 函数以在 Promise 中抛出错误：

```js
let authorized = false;

function getUserById(id) {
    return new Promise((resolve, reject) => {
        if (!authorized) {
            throw new Error('Unauthorized access to the user data');
        }

        resolve({
            id: id,
            username: 'admin'
        });
    });
}
```

And consume the promise:

```js
try {
    getUserById(10)
        .then(user => console.log(user.username))
        .catch(err => console.log(`Caught by .catch ${err}`));
} catch (error) {
    console.log(`Caught by try/catch ${error}`); // Caught by .catch Error: Unauthorized access to the user data
}
```

如果在 Promise 中抛出错误，Promise 的对象方法 catch() 方法将捕获它，而不是 try/catch 块。

如果链接 Promise，catch() 方法将捕获任何 Promise 中发生的错误。例如：

```js
promise1
    .then(promise2)
    .then(promise3)
    .then(promise4)
    .catch(err => console.log(err));
```

## Calling `reject()` function

Throwing an error has the same effect as calling the `reject()` as illustrated in the following example:

```js
let authorized = false;

function getUserById(id) {
    return new Promise((resolve, reject) => {
        if (!authorized) {
            reject('Unauthorized access to the user data');
        }

        resolve({
            id: id,
            username: 'admin'
        });
    });
}

try {
    getUserById(10)
        .then(user => console.log(user.username))
        .catch(err => console.log(`Caught by .catch ${err}`));
} catch (error) {
    console.log(`Caught by try/catch ${error}`);
}
```

In this example, instead of throwing an error inside the promise, we called the `reject()` explicitly. The `catch()` method also handles the error in this case.

## Missing the catch() method

以下示例没有提供 catch() 方法来处理 Promise 内的错误。它将导致运行时错误并终止程序：

```js
function getUserById(id) {
    return new Promise((resolve, reject) => {
        if (!authorized) {
            reject('Unauthorized access to the user data');
        }
        resolve({
            id: id,
            username: 'admin'
        });
    });
}

try {
    getUserById(10)
        .then(user => console.log(user.username));
} catch (error) {
    console.log(`Caught by try/catch ${error}`);
}
```

输出：

```js
Uncaught (in promise) Unauthorized access to the user data
```

If the promise is resolved, you can omit the `catch()` method. In the future, a potential error may cause the program to stop unexpectedly.