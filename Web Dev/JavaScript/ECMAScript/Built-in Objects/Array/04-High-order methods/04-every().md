# JavaScript Array every: Determining If All Array Elements Pass a Test

## Checking array elements using the `for` loop

Sometimes, you need to test whether every element of an array satisfies a specified condition.

通常，使用 for 循环来迭代所有元素并根据条件检查每个单独的元素。

```js
let numbers = [1, 3, 5];
```

检查 numbers 数组中的每个元素是否都大于零：

```js
let numbers = [1, 3, 5];
let result = true;
for (let i = 0; i < numbers.length; i++) {
    if (numbers[i] <= 0) {
        result = false;
        break;
    }
}
console.log(result);
```

This code is simple and straight forward. However, it is quite verbose.

JavaScript 数组类型提供 every() 方法，以更短、更清晰的方式检查数组的每个元素是否通过测试。

## Introduction to JavaScript Array `every()` method

从 ES5 开始，JavaScript 数组类型提供了 every() 方法来测试数组中的每个元素。

```js
let numbers = [1, 3, 5];
let result = numbers.every(function (e) {
    return e > 0;
});
console.log(result); // true
```

```js
let numbers = [1, 3, 5];
let result = numbers.every( e  => e > 0);
console.log(result); // true
```

every() 方法的语法：

```js
every(predicate: (value: any, index: number, array: any[]) => unknown, thisArg?: any): boolean
// predicate: A function that accepts up to three arguments. The every method calls the predicate function for each element in the array until the predicate returns a value which is coercible to the Boolean value false, or until the end of the array.
// thisArg: An object to which the this keyword can refer in the predicate function. If thisArg is omitted, undefined is used as the this value.
// Determines whether all the members of an array satisfy the specified test.
```

The `every()` method returns `true` if the `callback` function returns a truthy value for every array element; otherwise, it returns `false`.

Note that the `every()` method executes the `callback()` function on every element in the array until it finds the one that causes the `callback()` return a falsy value.

In other words, the `every()` will stop calling the `callback()` function and return `false` once there is an array element that causes `callback()` to return a falsy value.

## More JavaScript Array `every()` method examples

```js
let numbers = [1, 3, 5]
let range = {
  min: 0,
  max: 10,
}
let isInRange = numbers.every(function (e) {
  return e >= this.min && e <= this.max
}, range)
console.log(isInRange) // true
```

In this example, we pass the `range` object to the `every()` method as the second argument. And inside the `callback()` function, we reference the `range` object using the `this` keyword.

## Caution: Empty arrays

If you call the `every()` method on an empty array, the method will always return `true` for any condition.

```js
let gtZero = [].every(e => e > 0); // any condition
let ltZero = [].every(e => e < 0); // any condition

console.log('gtZero:', gtZero); // true
console.log('ltZero:', ltZero); // true
```