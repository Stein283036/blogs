# JavaScript Array reduce & reduceRight: Reducing an Array Into a Value

## Introduction to the JavaScript Array reduce() method

```js
let numbers = [1, 2, 3];
```

计算 numbers 数组元素的和。

使用 for 循环来迭代元素并将它们相加：

> bad style

```js
let numbers = [1, 2, 3];
let sum = 0;
for (let i = 0; i < numbers.length; i++) {
    sum += numbers[i];
}
console.log(sum);
```

The `Array.prototype` allows you to reduce an array to a single value using the `reduce()` method like this:

```js
let numbers = [1, 2, 3];
let sum = numbers.reduce(function (previousValue, currentValue) {
    return previousValue + currentValue;
});
console.log(sum);
```

## JavaScript Array reduce() method in detail

```js
array.reduce(callbackFn [, initialValue])
```

The `reduce()` method takes two arguments:

- A callback function `callbackFn`. The function is often referred to as a reducer.
- An optional initial value.

Calls the specified callback function for all the elements in an array. The return value of the callback function is the accumulated result, and is provided as an argument in the next call to the callback function.

### The callbackFn() function argument

```js
function callbackFn(previousValue, currentValue, currentIndex, array) { /**/}
```

### The initialValue argument

The `initialValue` argument is optional.

If you specify the `initialValue`, the `callbackFn` function will initialize the `previousValue` to the `initialValue` and `currentValue` to the first array’s element on the first call.

If you **don’t** specify the `initialValue`, the the `callbackFn` function will initialize the `previousValue` to the first array’s element (`array[0]`) in the array and the `currentValue` to the second array’s element (`array[1]`).

The following table illustrates the logic when the `reduce()` method executes the `callbackFn()` function for the first time according to the `initialValue` argument:

| `initialValue` | `previousValue` | `currentValue` |
| :------------- | :-------------- | :------------- |
| passed         | `initialValue`  | `array[0]`     |
| not passed     | `array[0]`      | `array[1]`     |

## More JavaScript Array reduce() examples

```js
let shoppingCart = [
  {
    product: 'phone',
    qty: 1,
    price: 500,
  },
  {
    product: 'Screen Protector',
    qty: 1,
    price: 10,
  },
  {
    product: 'Memory Card',
    qty: 2,
    price: 20,
  },
];
```

To calculate the total amount of the products in the shopping cart, you can use the `reduce()` method, like this:

```js
let total = shoppingCart.reduce(function (previousValue, currentValue) {
  return previousValue + currentValue.qty * currentValue.price;
}, 0);
console.log(total); // 550
```

Notice that in this example, we passed in the `initialValue` argument to the `reduce()` method.

If we didn’t do so, the `reduce()` method would take the first element of the `shoppingCart` array, which is an object, as an initial value and perform the calculation on this object. Hence, it would cause an incorrect result.

## JavaScript Array reduceRight() method

The `reduceRight()` method works in the same way as the `reduce()` method, but in the opposite direction.

The `reduce()` method starts at the first element and travels toward the last, whereas the `reduceRight()` method starts at the last element and travels backward the first.

```js
let numbers = [1, 2, 3];
let sum = numbers.reduceRight(function (previousValue, currentValue) {
  console.log({ previousValue, currentValue });
  return previousValue + currentValue;
});
console.log(`Result:${sum}`);
```

输出：

```js
{ previousValue: 3, currentValue: 2 }
{ previousValue: 5, currentValue: 1 }
Result:6
```