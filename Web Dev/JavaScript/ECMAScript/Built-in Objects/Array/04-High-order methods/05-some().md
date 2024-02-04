# JavaScript Array some: Check If at Least one Array Element Passes a Test

## Introduction to the JavaScript Array `some()` method

Sometimes, you want to check if an array has at least one element that meets a specified condition.

例如，检查以下数组是否至少有一个元素小于 5：

```js
let marks = [ 4, 5, 7, 9, 10, 3 ];
```

```js
let marks = [ 4, 5, 7, 9, 10, 3 ];
let lessThanFive = marks.some(e => e < 5);
console.log(lessThanFive); // true
```

## JavaScript Array `some()` syntax

```js
some(predicate: (value: any, index: number, array: any[]) => unknown, thisArg?: any): boolean
// predicate: A function that accepts up to three arguments. The some method calls the predicate function for each element in the array until the predicate returns a value which is coercible to the Boolean value true, or until the end of the array.
// thisArg: An object to which the this keyword can refer in the predicate function. If thisArg is omitted, undefined is used as the this value.
// Determines whether the specified callback function returns true for any element of an array.
```

## JavaScript Array `some()` examples

### Check if an element exists in the array

```js
function exists(value, arr) {
  // return arr.some((e) => e === value)
  return Array.prototype.some.call(arr, (num) => num === value)
}
let marks = [4, 5, 7, 9, 10, 2]
console.log(exists(4, marks)) // true
console.log(exists(11, marks)) // false
```

### Check if an array has one element that is in a range

```js
let marks = [4, 5, 7, 9, 10, 2];
const range = {
    min: 8,
    max: 10
};
let result = marks.some(function (e) {
    return e >= this.min && e <= this.max;
}, range);
console.log(result); // true
```

## Caution: Empty arrays

If you call the `some()` method on an empty array, the result is always `false` regardless of any condition.

```js
let result = [].some(e => e > 0);
console.log(result); // false
result = [].some(e => e <= 0);
console.log(result); // false
```