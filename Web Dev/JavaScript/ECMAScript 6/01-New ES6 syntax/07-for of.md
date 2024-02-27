# JavaScript for…of Loop

## Introduction to the JavaScript for…of loop

ES6 引入了一个新的语句 for...of 来迭代可迭代对象：

- Built-in Array, String, Map, Set, …
- Array-like objects such as arguments or NodeList
- User-defined objects that implement the iterator protocol.

for...of 的语法：

```js
for (variable of iterable) {
   // ...
}
```

## JavaScript for of loop examples

### Iterating over arrays

```js
let scores = [80, 90, 70];

for (let score of scores) {
    score = score + 5;
    console.log(score);
}
```

如果不更改循环内的变量，则应使用 const 关键字而不是 let 关键字：

```js
let scores = [80, 90, 70];

for (const score of scores) {
    console.log(score);
}
```

要访问循环内数组元素的索引，可以将 for...of 语句与数组的 entries() 方法结合使用。

array.entries() 方法在每次迭代中返回一对 [index, element]。

```js
let colors = ['Red', 'Green', 'Blue'];

for (const [index, color] of colors.entries()) {
    console.log(`${color} is at index ${index}`);
}
```

在此示例中，使用了数组解构将 entries() 方法的结果分配给每次迭代中的 index 和 color 变量。

### In-place object destructuring with for…of

```js
const ratings = [
    {user: 'John',score: 3},
    {user: 'Jane',score: 4},
    {user: 'David',score: 5},
    {user: 'Peter',score: 2},
];

let sum = 0;
for (const {score} of ratings) {
    sum += score;
}

console.log(`Total scores: ${sum}`); // 14
```

- The `ratings` is an array of objects. Each object has two properties user and score.
- The `for...of` iterate over the `ratings` array and calculate the total scores of all objects.
- The expression const {score} of ratings uses object destructing to assign the score property of the current iterated element to the score variable.

### Iterating over strings

```js
let str = 'abc';
for (let c of str) {
    console.log(c);
}
```

### Iterating over Map objects

```js
let colors = new Map();

colors.set('red', '#ff0000');
colors.set('green', '#00ff00');
colors.set('blue', '#0000ff');

for (let color of colors) {
    console.log(color);
}
```

输出：

```js
[ 'red', '#ff0000' ]
[ 'green', '#00ff00' ]
[ 'blue', '#0000ff' ]
```

### Iterating over set objects

```js
let nums = new Set([1, 2, 3]);

for (let num of nums) {
    console.log(num);
}
```

## `for...of` vs. `for...in`

JavaScript 中的 `for...in` 循环会迭代对象的所有可枚举属性，包括对象自身的属性以及其原型链上的属性。这意味着 `for...in` 循环会遍历对象自身的属性，同时也会遍历其原型链上可枚举的属性。如果想要避免遍历原型链上的属性，可以使用 `Object.hasOwnProperty()` 方法来过滤出对象自身的属性。

for...in 迭代对象的所有可枚举属性。它不会迭代 Array、Map 或 Set 等集合。

与 for...in 循环不同，for...of 迭代一个集合，而不是一个对象。事实上，for...of 会迭代任何具有 [Symbol.iterator] 属性的集合的元素。

数组是一种特殊的对象，它的属性名是数字索引，而属性值则是数组中的元素。

```js
let scores = [10,20,30];
scores.message = 'Hi';

console.log("for...in:");
for (let score in scores) {
  console.log(score); 
}

console.log('for...of:');
for (let score of scores) {
  console.log(score);
}
```

输出：

```js
for...in:
0
1
2
message
for...of:
10
20
30
```

在此示例中，for...in 语句迭代 scores 数组的属性，而 for...of 则迭代数组的元素。