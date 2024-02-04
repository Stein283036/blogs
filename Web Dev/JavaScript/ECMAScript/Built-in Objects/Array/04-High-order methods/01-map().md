# JavaScript Array map: Transforming Elements

## Introduction to JavaScript Array `map()` method

Sometimes, you need to take an array, transform its elements, and include the results in a new array.

通常，使用 for 循环来迭代元素，转换每个元素，并将结果添加到一个新数组中。

有一个数字数组，其中每个元素代表圆的半径，如下所示：

```js
let circles = [
    10, 30, 50
];
```

计算每个圆的面积并将结果添加到到新数组中。

```js
let areas = []; // to store areas of circles
let area = 0;
for (let i = 0; i < circles.length; i++) {
    area = Math.floor(Math.PI * circles[i] * circles[i]);
    areas.push(area);
}
console.log(areas);
```

从 ES5 开始，JavaScript 数组类型提供了 map() 方法，以更简洁的方式转换数组元素。

```js
function circleArea(radius) {
    return Math.floor(Math.PI * radius * radius);
}
let areas = circles.map(circleArea);
console.log(areas); // [314, 2827, 7853]
```

为了使其更短，可以向 map() 方法传递一个匿名函数：

```js
let areas = circles.map(function(radius){
    return Math.floor(Math.PI * radius * radius);
});
console.log(areas);
```

可以利用 ES6 中的箭头函数以更简洁的代码实现相同的结果：

```js
let areas = circles.map(radius => Math.floor(Math.PI * radius * radius));
console.log(areas);
```

## JavaScript Array map() method in detail

```js
map(callbackfn: (value: any, index: number, array: any[]) => any, thisArg?: any): any[]
// calllbackfn: A function that accepts up to three arguments. The map method calls the callbackfn function one time for each element in the array.
// thisArg: An object to which the this keyword can refer in the callbackfn function. If thisArg is omitted, undefined is used as the this value.
// Calls a defined callback function on each element of an array, and returns an array that contains the results.
```

The `callback()` function takes three arguments:

- The `value` is the current element of the array that is being processed.
- The `index` is the index of the `value`.
- The `array` is the array object being traversed.

The `value` is required while the `index` and `array` arguments are optional.

If you pass the `thisArg` to the `map()` method, you can reference the `contextObject` inside the `callback()` function using the `this` keyword.

需要注意的是，map() 方法不会更改原始数组，它会创建一个由回调函数转换的所有元素组成的新数组。

## More JavaScript Array `map()` examples

```js
let numbers = [16, 25, 36];
let results = numbers.map(Math.sqrt);
console.log(results); //  [4, 5, 6]
```