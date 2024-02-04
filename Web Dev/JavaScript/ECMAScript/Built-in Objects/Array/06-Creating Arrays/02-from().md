# JavaScript Array.from()

## Introduction to JavaScript Array.from() method

要在 ES5 中从 array-like object 中创建数组，可以迭代所有数组元素并将它们中的每个元素添加到中间数组中：

```js
function arrayFromArgs() {
    var results = [];
    for (var i = 0; i < arguments.length; i++) {
        results.push(arguments[i]);
    }
    return results;
}
var fruits = arrayFromArgs('Apple', 'Orange', 'Banana');
console.log(fruits);
```

为了使其更简洁，可以使用 Array.prototype 的 slice() 方法：

```js
function arrayFromArgs() {
    return Array.prototype.slice.call(arguments);
}
var fruits = arrayFromArgs('Apple', 'Orange', 'Banana');
console.log(fruits);
```

ES6 引入了 Array.from() 方法，该方法从 array-like 或 iterable object 创建 Array 的新实例。

```js
Array.from(target [, mapFn[, thisArg]])
```

target 是一个要转换为数组的 array-like 或 iterable object。

mapFn 是调用数组每个元素的映射函数。

thisArg 是执行 mapFn 函数时的 this 值。

Array.from() 返回一个新的 Array 实例，其中包含目标对象的所有元素。

## JavaScript Array.from() method examples

### Create an array from an array-like object

```js
function arrayFromArgs() {
    return Array.from(arguments);
}

console.log(arrayFromArgs(1, 'A'));
```

### JavaScript Array `Array.from()` with a mapping function

Array.from() 方法接受一个回调函数，该函数对正在创建的数组的每个元素执行映射函数。

```js
function addOne() {
    return Array.from(arguments, x => x + 1);
}
console.log(addOne(1, 2, 3));
```

### JavaScript Array.from() with a this value

如果映射函数属于一个对象，可以选择将第三个参数传递给 Array.from() 方法。该对象将表示映射函数内的 this 值。

```js
let doubler = {
    factor: 2,
    double(x) {
        return x * this.factor;
    }
}
let scores = [5, 6, 7];
let newScores = Array.from(scores, doubler.double, doubler);
console.log(newScores); // [ 10, 12, 14 ]
```

### Create an array from an iterable object

由于 Array.from() 方法也适用于可迭代对象，因此可以使用它从具有 [symbol.iterator] 属性的任何对象创建数组。

```js
let even = {
    *[Symbol.iterator]() {
        for (let i = 0; i < 10; i += 2) {
            yield i;
        }
    }
};
let evenNumbers = Array.from(even);
console.log(evenNumbers); // [0, 2, 4, 6, 8]
```