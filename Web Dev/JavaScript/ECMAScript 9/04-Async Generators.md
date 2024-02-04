# JavaScript Async Generators

## What is an async generator

An async generator is similar to a regular generator except that its next() method returns a **Promise**. To iterate over an async generator, you use the for await...of statement.

## Introduction to the JavaScript async generators

常规生成器是一个可以中途暂停并从暂停处继续的函数。

```js
function* sequence(start, end) {
    for (let i = start; i <= end; i++) {
        yield i;
    }
}

let seq = sequence(1, 5);

for (const num of seq) {
    console.log(num);
}
```

异步生成器与常规生成器类似，但有以下区别：

- async 关键字放在 function 关键字前面。
- yield 返回一个 Promise ，而不是一个 value。 Promise 通常是异步操作的包装器。

generator `sequence` to the async generator `asyncSequence`

```js
async function* asyncSequence(start, end) {
    for (let i = start; i <= end; i++) {
        yield new Promise((resolve, reject) => {
            setTimeout(() => {
                resolve(i);
            }, 1000);
        });

    }
}
```

要迭代整个异步生成器，可以使用 for wait...of 语句。

由于只能在 async function 中使用 await 关键字，因此将代码包装在异步IIFE中，如下所示：

```js
(async () => {
    let seq = asyncSequence(1, 5);

    for await (let num of seq) {
        console.log(num);
    }
})();
```

The async generators can be very useful when you access a stream of data and want to report the progress like using a progress bar.
