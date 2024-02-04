# JavaScript Promise.race()

## Introduction to JavaScript Promise.race() static method

Promise.race() 静态方法接受一系列 Promise 作为可迭代对象，并在有一个 Promise 被解析或拒绝时返回一个新的 Promise，该 Promise 会立即解析或拒绝，并包含该 Promise 的值（fulfilled）或原因（rejected）。

Promise.race() 方法的语法：

```js
Promise.race(iterable)
```

在此语法中，iterable 是一个包含 Promise 列表的可迭代对象。

Promise.race() 的名称意味着所有的 Promise 都相互竞争，只有一个获胜者，无论是被解析还是被拒绝。

![img](https://www.javascripttutorial.net/wp-content/uploads/2022/02/JavaScript-Promise-Race-Fulfilled.svg)

在此图中：

- The `promise1` is fulfilled with the value `v1` at `t1`.
- The `promise2` is rejected with the `error` at `t2`.
- Because the `promise1` is resolved earlier than the `promise2`, the `promise1` wins the race. Therefore, the `Promise.race([promise1, promise2])` returns a new promise that is fulfilled with the value `v1` at `t1`.

## JavaScript Promise.race() examples

### Simple JavaScript Promise.race() examples

下面创建了两个 Promise：一个在 1 秒内解析，另一个在 2 秒内解析。由于第一个 Promise 的解析速度比第二个 Promise 快，因此 Promise.race() 使用第一个 Promise 的值进行解析：

```js
const p1 = new Promise((resolve, reject) => {
    setTimeout(() => {
        console.log('The first promise has resolved');
        resolve(10);
    }, 1 * 1000);

});

const p2 = new Promise((resolve, reject) => {
    setTimeout(() => {
        console.log('The second promise has resolved');
        resolve(20);
    }, 2 * 1000);
});


Promise.race([p1, p2])
    .then(value => console.log(`Resolved: ${value}`))
    .catch(reason => console.log(`Rejected: ${reason}`));
```

输出：

```js
The first promise has resolved
Resolved: 10
The second promise has resolved
```

以下示例创建了两个 Promise。第一个 Promise 在 1 秒内解析，而第二个 Promise 在 2 秒内拒绝。由于第一个 Promise 比第二个 Promise 更快，因此返回的 Promise 解析为第一个 Promise 的值：

```js
const p1 = new Promise((resolve, reject) => {
    setTimeout(() => {
        console.log('The first promise has resolved');
        resolve(10);
    }, 1 * 1000);

});

const p2 = new Promise((resolve, reject) => {
    setTimeout(() => {
        console.log('The second promise has rejected');
        reject(20);
    }, 2 * 1000);
});


Promise.race([p1, p2])
    .then(value => console.log(`Resolved: ${value}`))
    .catch(reason => console.log(`Rejected: ${reason}`));
```

输出：

```js
The first promise has resolved
Resolved: 10
The second promise has rejected
```

如果第二个 Promise 比第一个 Promise 更快，则返回 Promise 将因第二个 Promise 的原因而拒绝。