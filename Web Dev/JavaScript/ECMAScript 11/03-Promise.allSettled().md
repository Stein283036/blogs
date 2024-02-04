# JavaScript Promise.allSettled()

## Introduction to the `Promise.allSettled()` method

ES2020 introduced the Promise.allSettled() method that accepts a list of Promises and returns a new promise that resolves after all the input promises have settled, either resolved or rejected.

Promise.allSettled() 方法的语法：

```js
Promise.allSettled(iterable);
```

The `iterable` contains the promises. The `Promise.allSettled()` returns a **pending promise** that will be asynchronously fulfilled once every input promise has settled.

The Promise.allSettled() method returns a promise that resolves to an array of objects that each describes the result of the input promise.

Each object has two properties: `status` and `value` (or `reason`).

- The `status` can be either `fulfilled` or `rejected`.
- The `value` if case the promise is fulfilled or `reason`) if the promise is rejected.

The following diagram illustrates how the `Promise.allSettled()` method works:

![JavaScript Promise.allSettled](https://www.javascripttutorial.net/wp-content/uploads/2022/02/JavaScript-Promise.allSettled.svg)

## JavaScript Promise.allSettled() example

The following example uses the `Promise.allSettled()` to wait for all the input Promises to settle:

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

Promise.allSettled([p1, p2])
    .then((result) => {
        console.log(result);
    });
```

Output:

![img](D:\2024年\blogs\Web Dev\JavaScript\ECMAScript\07-Promise && async-await\assets\allSettled.png)