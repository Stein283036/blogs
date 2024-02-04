# JavaScript Array includes: Check If an Element is in the Array

## Introduction to the JavaScript Array `includes()` method

使用数组时，经常想要检查数组是否包含元素。可以使用 indexOf() 方法：

```js
let numbers = [1,2,3];
if(numbers.indexOf(2) !== -1){
   // process here
}
```

As you can see, the `indexOf()` method doesn’t really clearly state what it means. In addition, the `indexOf()` uses strict equality operator (`===`) for comparison, therefore, it doesn’t work with `NaN` as shown in the following example:

```js
[NaN].indexOf(NaN); // -1
```

To work around this, developers came up with a **helper function**, for example, `Lodash` provides the `_.incudes()` method that checks if a value is in the array.

ECMAScript 2016 standardized this functionality by providing the `Array.prototype.includes()` method.

The `includes()` method returns `true` if an array contains a given element; Otherwise, it returns `false`.

```js
includes(searchElement: any, fromIndex?: number): boolean
// Determines whether an array includes a certain element, returning true or false as appropriate.
```

```js
[1,2,3].includes(2); // true
[1,2,3].includes(4); // false
[1,2,3].includes(1,1); // false
```

Unlike the `indexOf()` method, the `includes()` method works perfectly fine with the `NaN`:

```js
[NaN].includes(NaN); // true
```

Note that the `includes()` doesn’t distinguish between `+0` and `-0` as shown in the following example:

> Object.is() 方法区分 +0 和 -0

```js
[-0].includes(+0); // true
```

The following example demonstrates how to use the `includes()` method to check if an object is in an array.

```js
let bmw = {name: 'BMW' }, 
    toyota = { name: 'Toyota'},
    ford = {name: 'Ford'}

let cars = [ford, toyota];

console.log(cars.includes(ford)); // true
console.log(cars.includes(bmw)); // false
```