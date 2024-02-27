# The Essential Guide to JavaScript Iterators

## The `for` loop issues

当有数据数组时，通常使用 for 循环来迭代其元素。

```js
let ranks = ['A', 'B', 'C'];

for (let i = 0; i < ranks.length; i++) {
    console.log(ranks[i]);
}
```

for 循环使用变量 i 来跟踪 ranks 数组的索引。只要 i 的值小于 ranks 数组中的元素数量，每次执行循环时，i 的值都会递增。

这段代码很简单。然而，当将一个循环嵌套在另一个循环中时，它的复杂性就会增加。此外，跟踪循环内的多个变量很容易出错。

ES6 引入了一种名为 for...of 的新循环结构，以消除标准循环的复杂性并避免因跟踪循环索引而导致的错误。

要迭代ranks数组的元素，可以使用以下for...of构造：

```js
for(let rank of ranks) {
    console.log(rank);
}
```

for...of 比 for 循环优雅得多，因为它显示了代码的真正意图 - 迭代数组以访问序列中的每个元素。

除此之外，for...of 循环能够在任何**可迭代**对象上创建循环，而不仅仅是数组。

要了解可迭代对象（iterable object），需要首先了解迭代协议。

## Iteration protocols

有两种迭代协议：**iterable protocol** 和 **iterator protocol**。

### Iterator protocol

An object is an iterator when it implements an interface (or API) that answers two questions:

- Is there any element left?
- If there is, what is the element?

Technically speaking, an object is qualified as an iterator when it has a `next()` method that returns an object with two properties:

- `done`: a boolean value indicating whether or not there are any more elements that could be iterated upon.
- `value`: the current element.

Each time you call the `next()`, it returns the next value in the collection:

```js
{ value: 'next value', done: false }
```

If you call the `next()` method after the last value has been returned, the `next()` returns the result object as follows:

```js
{done: true: value: undefined}
```

The value of the `done` property indicates that there is no more value to return and the `value` of the property is set to `undefined`.

### Iterable protocol

An object is iterable when it contains a method called `[Symbol.iterator]` that takes no argument and returns an object that conforms to the iterator protocol.

The [Symbol.iterator] is one of the built-in well-known symbols in ES6.

## Iterators

Since ES6 provides built-in iterators for the collection types  Array, Set, and Map, you don’t have to create iterators for these objects.

If you have a custom type and want to make it iterable so that you can use the `for...of` loop construct, you need to implement the iteration protocols.

The following code creates a `Sequence` object that returns a list of numbers in the range of ( `start`, `end`) with an `interval` between subsequent numbers.

```js
class Sequence {
    constructor( start = 0, end = Infinity, interval = 1 ) {
        this.start = start;
        this.end = end;
        this.interval = interval;
    }
    [Symbol.iterator]() {
        let nextIndex = this.start;
        return  {
            next: () => {
                if ( nextIndex <= this.end ) {
                    let result = { value: nextIndex,  done: false };
                    nextIndex += this.interval;
                    return result;
                }
                return { value: undefined, done: true };
            }
        }
    }
};
```

The following code uses the `Sequence` iterator in a `for...of` loop:

```js
let evenNumbers = new Sequence(2, 10, 2);

for (const num of evenNumbers) {
    console.log(num);
}
2
4
6
8
10
```

You can explicitly access the `[Symbol.iterator]()` method as shown in the following script:

```js
let evenNumbers = new Sequence(2, 10, 2);
let iterator = evenNumbers[Symbol.iterator]();

let result = iterator.next();

while( !result.done ) {
    console.log(result.value);
    result = iterator.next();
}
```

## Cleaning up

In addition to the `next()` method, the `[Symbol.iterator]()` may optionally return a method called `return()`.

The `return()` method is invoked automatically when the iteration is stopped prematurely. It is where you can place the code to clean up the resources.

The following example implements the `return()` method for the `Sequence` object:

```js
class Sequence {
    constructor( start = 0, end = Infinity, interval = 1 ) {
        this.start = start;
        this.end = end;
        this.interval = interval;
    }
    [Symbol.iterator]() {
        let counter = 0;
        let nextIndex = this.start;
        return  {
            next: () => {
                if ( nextIndex <= this.end ) {
                    let result = { value: nextIndex,  done: false }
                    nextIndex += this.interval;
                    counter++;
                    return result;
                }
                return { value: counter, done: true };
            },
            return: () => {
                console.log('cleaning up...');
                return { value: undefined, done: true };
            }
        }
    }
}
```

以下代码片段使用 Sequence 对象生成从 1 到 10 的奇数序列。但是，它会过早停止迭代。结果，return() 方法被自动调用。

```js
let oddNumbers = new Sequence(1, 10, 2);

for (const num of oddNumbers) {
    if( num > 7 ) {
        break;
    }
    console.log(num);
}
1
3
5
7
cleaning up...
```

## iterable and array-like

这两个官方术语看起来差不多，但其实大不相同。请确保你能够充分理解它们的含义，以免造成混淆。

- **Iterable** 如上所述，是实现了 `Symbol.iterator` 方法的对象。
- **Array-like** 是有索引和 `length` 属性的对象，所以它们看起来很像数组。

当我们将 JavaScript 用于编写在浏览器或任何其他环境中的实际任务时，我们可能会遇到可迭代对象或类数组对象，或两者兼有。

例如，字符串即是可迭代的（`for..of` 对它们有效），又是类数组的（它们有数值索引和 `length` 属性）。

但是一个可迭代对象也许不是类数组对象。反之亦然，类数组对象可能不可迭代。
