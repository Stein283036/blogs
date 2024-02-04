# JavaScript Promise.all()

## Introduction to the JavaScript Promise.all() method

Promise.all() 静态方法接收可迭代的 Promise：

```js
Promise.all(iterable);
```

Promise.all() 方法返回一个单一的 Promise，当所有输入的 Promise 都得到解析时，该 Promise 就会解析。返回的 Promise 解析为输入 Promise 结果的数组：

![img](https://www.javascripttutorial.net/wp-content/uploads/2022/02/JavaScript-Promise.all-Fulfilled-1.svg)

在此图中，promise1 在 t1 解析为值 v1，promise2 在 t2 解析为值 v2。因此，Promise.all(promise1,promise2)返回一个promise，该promise解析为一个包含promise1和promise2[v1,v2]在t2的结果的数组。

换句话说，Promise.all() 等待所有输入 Promise 解析并返回一个新 Promise，新的 Promise 解析为包含所有输入 Promise 结果的数组。

如果其中一个输入 Promise 被拒绝，Promise.all() 方法会立即返回一个被拒绝的 Promise，并显示第一个被拒绝的 Promise 的错误：

![JavaScript Promise.all Rejected](https://www.javascripttutorial.net/wp-content/uploads/2022/02/JavaScript-Promise.all-Rejected.svg)

在此图中，promise2 在 t1 处因错误而拒绝。因此，Promise.all() 返回一个新的 Promise，该 Promise 立即被拒绝并出现相同的错误。此外，Promise.all() 不关心其它输入的 Promise，无论它们会被解析还是被拒绝。

实践中，Promise.all() 对于聚合多个异步操作的结果很有用。

## JavaScript Promise.all() method examples

### Resolved promises example

以下 Promises 在 1、2 和 3 秒后解析为 10、20 和 30。我们使用setTimeout()来模拟异步操作：

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
const p3 = new Promise((resolve, reject) => {
  setTimeout(() => {
    console.log('The third promise has resolved');
    resolve(30);
  }, 3 * 1000);
});

Promise.all([p1, p2, p3]).then((results) => {
  // results = [ 10, 20, 30 ]
  const total = results.reduce((p, c) => p + c);

  console.log(`Results: ${results}`);
  console.log(`Total: ${total}`);
});
```

输出：

```js
The first promise has resolved
The second promise has resolved
The third promise has resolved
Results: 10,20,30
Total: 60
```

当所有 Promise 都得到解析后，这些 Promise 中的值将作为数组传递到 then() 方法的回调中。

### Rejected promises example

Promise.all() 返回一个 Promise，如果任何输入的 Promise 被拒绝，该 Promise 也会被拒绝。

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
        reject('Failed');
    }, 2 * 1000);
});
const p3 = new Promise((resolve, reject) => {
    setTimeout(() => {
        console.log('The third promise has resolved');
        resolve(30);
    }, 3 * 1000);
});


Promise.all([p1, p2, p3])
    .then(console.log) // never execute
    .catch(console.log);
```

输出：

```js
The first promise has resolved
The second promise has rejected
Failed
The third promise has resolved
```

在这段代码中，虽然 `p2` 的 Promise 被拒绝（rejected），但是 `Promise.all()` 方法仍然会等待所有的 Promise 都解决（resolve）或至少有一个被拒绝（rejected）后才会执行。这意味着即使有一个 Promise 被拒绝，其他 Promise 仍然会继续执行，并且 `Promise.all()` 方法会等待所有的 Promise 结束后才返回。