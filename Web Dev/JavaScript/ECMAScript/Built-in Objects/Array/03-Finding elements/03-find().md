# JavaScript Array find() Method

## Introduction to the Array find() method

在 ES5 中，要查找数组中的元素，可以使用 indexOf() 或 lastIndexOf() 方法。但是，这些方法非常有限，因为它们仅返回第一个匹配元素的索引。

ES6 引入了一个名为 find() 的新方法，添加到 Array.prototype 对象中。

find() 方法返回数组中通过 test function 的第一个元素。

```js
find(callback(element[, index[, array]])[, thisArg])
```

### Arguments

find() 接受两个参数：一个回调函数和一个用于回调函数内的 this 的可选值。

### `callback`

回调是执行数组每个元素的函数。它需要三个参数：

- `element` is the current element.
- `index` the index of the current element.
- `array` the array that the `find()` was called upon.

### `thisArg`

thisArg 是回调中用作 this 的对象。

### Return value

find() 对数组中的每个元素执行回调函数，直到回调返回真值（truthy value）。

如果回调返回真值，则 find() 立即返回该元素并停止搜索。否则，它返回 undefined。

如果要查找找到的元素的索引，可以使用 findIndex() 方法。

## JavaScript find() examples

以下示例使用 find() 方法搜索数字数组中的第一个偶数：

```js
let numbers = [1, 2, 3, 4, 5];

console.log(numbers.find(e => e % 2 == 0));
```

Suppose that we have a list of customer objects with `name` and `credit` properties as follows:

```js
let customers = [{
    name: 'ABC Inc',
    credit: 100
}, {
    name: 'ACME Corp',
    credit: 200
}, {
    name: 'IoT AG',
    credit: 300
}];
```

The following code uses the `find()` method to find the first customer whose credit is greater than 100.

```js
console.log(customers.find(c => c.credit > 100)); // { name: 'ACME Corp', credit: 200 }
```

使用 `thisArg` 的示例：

```js
let obj = {
  base: 250,
  index: 0,
}

let res = customers.find(function (customer) {
  return customer.credit > obj.base
}, obj)

console.log(res) // { name: 'IoT AG', credit: 300 }
```