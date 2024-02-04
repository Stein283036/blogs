# JavaScript Array findIndex() Method

## Introduction to the JavaScript Array findIndex() Method

ES6 在 Array.prototype 中添加了一个名为 findIndex() 的新方法，查找数组中满足所提供的测试函数的第一个元素。

findIndex() 方法返回满足测试函数的元素的索引，如果没有元素通过测试，则返回 -1。

```js
findIndex(testFn(element[, index[, array]])[, thisArg])
```

findIndex() 有两个参数：

### `testFn`

testFn 是一个对数组中的每个元素执行的函数，直到函数返回 true，表示已找到该元素。

testFn 有三个参数：

- `element` is the current element in the array.
- `index` is the index of the current element being processed.
- `array` is the array that the `findIndex()` was called upon.

### `thisArg`

thisArg 是一个可选对象，在执行回调时使用 this。如果省略 thisArg 参数，findIndex() 函数将使用 undefined。

findIndex() 对数组中的每个元素执行 testFn，直到找到 testFn 返回 true 值的元素。

一旦 findIndex() 找到这样的元素，它会立即返回该元素的索引。

## JavaScript Array findIndex() examples

### Using the Array findIndex() method with a simple array example

```js
let ranks = [1, 5, 7, 8, 10, 7];
let index = ranks.findIndex(rank => rank === 7);
console.log(index); // 2
```

### Using the Array findIndex() method with a more complex condition

```js
let ranks = [1, 5, 7, 8, 10, 7];

let index = ranks.findIndex(
    (rank, index) => rank === 7 && index > 2
);

console.log(index); // 5
```

### Using the Array findIndex() method with an array of objects

```js
const products = [
  { name: 'Phone', price: 999 },
  { name: 'Computer', price: 1999 },
  { name: 'Tablet', price: 995 },
];

const index = products.findIndex(product => product.price > 1000);

console.log(index); // 1
```