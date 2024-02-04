# JavaScript Array concat: Merge Arrays

To merge two or more arrays, you use the `concat()` method of an Array object. The `concat()` method returns a new array and doesn’t change the original arrays.

```js
let odds = [1,3,5];
let evens = [2,4,6];
// merge odds and evens array
let combined = odds.concat(evens);
console.log('Result:', combined); // Result: [ 1, 3, 5, 2, 4, 6 ]
console.log('Odds:', odds); // Odds: [ 1, 3, 5 ]
```

The `concat()` method allows you to merge more than two arrays as shown in the following example:

```js
let upper  = ['A','B','C'];
let lower  = ['a','b','c'];
let digits = [1,2,3];
let alphanumerics = upper.concat(lower, digits); // ['A', 'B', 'C', 'a',  'b', 'c', 1,   2,  3]
```

When you don’t pass any argument into the `concat()` method, it simply clones the array and returns it:

```js
let colors = ['red','green','blue'];
let rgb = colors.concat();
console.log(rgb); // [ 'red', 'green', 'blue' ]
```

If you pass values that are not arrays, into the `concat()` method, the method will appends each value to the end of the result array:

```js
let rgb = ['red','green','blue'];
let moreColors = rgb.concat('yellow','magento');
console.log(moreColors);
```

In ES6, you can use spread operator to merge multiple arrays as follows:

```js
let odds = [1,3,5];
let evens = [2,4,6];
let combined = [...odds, ...evens];
console.log(combined); // [ 1, 3, 5, 2, 4, 6 ]
```