# JavaScript Asynchronous Iterators

## Introduction to JavaScript Asynchronous Iterators

ES6 引入了迭代器接口，允许顺序访问数据。迭代器非常适合访问同步数据源，例如数组 array、集合 set 和映射 map。

迭代器接口的主要方法是 next()，它返回 {value, done} 对象，其中 done 是一个布尔值，指示是否到达序列末尾，value 是序列中的生成值。

同步数据意味着序列中的下一个 value 和 done 状态在 next() 方法返回时已知。

除了同步数据源之外，JavaScript 还经常需要访问异步数据源，例如 I/O 访问。对于异步数据源，迭代器的 value 和 done 状态在 next() 方法返回时通常是未知的。

为了处理异步数据源，ES2018 引入了 asynchronous iterator 接口。

An async iterator is like an iterator except that its next() method returns a **promise** that resolves to the {value, done} object.

The following illustrates the `Sequence` class that implements the iterator interface.

```js
class Sequence {
    constructor(start = 0, end = Infinity, interval = 1) {
            this.start = start;
            this.end = end;
            this.interval = interval;
        }
        [Symbol.iterator]() {
            let counter = 0;
            let nextIndex = this.start;
            return {
                next: () => {
                    if (nextIndex <= this.end) {
                        let result = {
                            value: nextIndex,
                            done: false
                        }
                        nextIndex += this.interval;
                        counter++;
                        return result;
                    }
                    return {
                        value: counter,
                        done: true
                    };
                }
            }
        }
}
```

To make this `Sequence` class asynchronously, you need to modify it as follows:

- Use the `Symbol.asyncIterator` instead of the `Symbol.iterator`
- Return a Promise from the `next()` method.

```js
class AsyncSequence {
    constructor(start = 0, end = Infinity, interval = 1) {
            this.start = start;
            this.end = end;
            this.interval = interval;
        }
        [Symbol.asyncIterator]() {
            let counter = 0;
            let nextIndex = this.start;
            return {
                next: async () => {
                    if (nextIndex <= this.end) {
                        let result = {
                            value: nextIndex,
                            done: false
                        }
                        nextIndex += this.interval;
                        counter++;

                        return new Promise((resolve, reject) => {
                            setTimeout(() => {
                                resolve(result);
                            }, 1000);
                        });
                    }
                    return new Promise((resolve, reject) => {
                        setTimeout(() => {
                            resolve({
                                value: counter,
                                done: true
                            });
                        }, 1000);

                    });
                }
            }
        }
}
```

The `AsyncSequence` returns the next number in the sequence after every 1 second.

## The `for await...of` statement

为了迭代异步可迭代对象，ES2018 引入了 for wait...of 语句：

```js
for await (variable of iterable) {
    // statement
}
```

由于只能在异步函数中使用 await 关键字，因此可以创建一个异步 IIFE：

```js
(async () => {

    let seq = new AsyncSequence(1, 10, 1);

    for await (let value of seq) {
        console.log(value);
    }

})();
```

下表说明了迭代器和异步迭代器之间的差异：

| #                        | Iterators         | Async iterators                            |
| :----------------------- | :---------------- | :----------------------------------------- |
| Well-known Symbol        | `Symbol.iterator` | `Symbol.asyncIterator`                     |
| `next()` return value is | `{value, done }`  | `Promise` that resolves to `{value, done}` |
| Loop statement           | `for...of`        | `for await...of`                           |
