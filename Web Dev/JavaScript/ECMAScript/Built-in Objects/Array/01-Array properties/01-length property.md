# JavaScript Array Length

## What exactly is the JavaScript Array length property

根据定义，数组的 length 属性是一个无符号的 32 位整数，其数值始终大于数组中的最高索引。

The `length` property behaves differently depending on the array types including dense and sparse.

### Dense arrays

A dense array is an array where its elements have contiguous indexes starting at zero.

For dense arrays, you can use the `length` property to get the number of elements in the array.

```js
let colors = ['red', 'green', 'blue'];
console.log(colors.length); // 3
```

When you empty the `colors` array, its length is zero:

```js
colors = [];
console.log(colors.length); // 0
```

### Sparse arrays

A sparse array is an array whose elements don’t have contiguous indexes starting at zero.

For example, the `[10,, 20, 30]` is a sparse array because the indexes of its elements are 0, 2, and 3.

In a sparse array, the length property doesn’t indicate the actual number of elements. It’s a number that is greater than the highest index.

```js
let numbers = [10, , 20, 30];
console.log(numbers.length); // 4
```

The following adds an element to the `numbers` array at the index 10:

```js
numbers[10] = 100;
console.log(numbers.length); // 11
console.log(numbers); // [ 10, <1 empty item>, 20, 30, <6 empty items>, 100 ]
```

## Modifying JavaScript Array length property

JavaScript allows you to change the value of the array `length` property. By changing the value of the length, you can remove elements from the array or make the array sparse.

### Empty an array

set length to zero, the array will be empty:

```js
const fruits = ['Apple', 'Orange', 'Strawberry'];
fruits.length = 0;
console.log(fruits); // []
```

### Remove elements

If you set the `length` property of an array to a value that is lower than the highest index, all the elements whose index is greater than or equal to the new length are removed.

```js
const fruits = ['Apple', 'Orange', 'Strawberry'];
fruits.length = 2;
console.log(fruits); // [ 'Apple', 'Orange' ]
```

### Make array sparse

If you set the `length` property of an array to a value that is higher than the highest index, the array will be spare.

```js
const fruits = ['Apple', 'Orange', 'Strawberry'];
fruits.length = 5;
console.log(fruits); // [ 'Apple', 'Orange', 'Strawberry', <2 empty items> 
```