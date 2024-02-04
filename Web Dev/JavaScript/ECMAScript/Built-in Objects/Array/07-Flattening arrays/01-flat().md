# JavaScript Array flat()

## Introduction to the JavaScript Array `flat()` method

ES2019 introduced the `Array.prototype.flat()` method that creates a new array with all the elements of the subarrays concatenated to it recursively up to a specified depth.

flat() 方法的语法：

```js
flat(depth?: 1): any[]
// depth: The maximum recursion depth
// Returns a new array with all sub-array elements concatenated into it recursively up to the specified depth.
```

The `depth` parameter specifies how deep the method flats the array structure. It defaults to 1.

```js
const numbers = [1, 2, [3, 4, 5]];
const flatNumbers = numbers.flat(0); // 不展开数组
console.log(flatNumbers); // [1, 2, [3, 4, 5]]
```

flat() 方法将嵌套数组 [3,4,5] 的所有元素连接到新数组的元素。

Note that the `flat()` method creates a new array and doesn’t change the original array:

```js
console.log(numbers); // [ 1, 2, [ 3, 4, 5 ] ]
```

The following example flats an array with two level depth:

```js
const numbers = [1, 2, [3, 4, 5, [6, 7]]];
const flatNumbers = numbers.flat(2);
console.log(flatNumbers); // [1, 2, 3, 4, 5, 6, 7]
```

When you don’t know the depth level, you can pass the `Infinity` into the `flat()` method to recursively concatenate all elements of the sub-arrays into the new array:

```js
const numbers = [1, 2, [3, 4, 5, [6, 7, [8, 9]]]];
const flatNumbers = numbers.flat(Infinity);
console.log(flatNumbers);
```

If an array has empty slots, you can use the `flat()` method to remove the holes, like this:

```js
const numbers = [1, 2, , 4, , 5];
const sequence = numbers.flat();
console.log(sequence); // [ 1, 2, 4, 5 ]
```