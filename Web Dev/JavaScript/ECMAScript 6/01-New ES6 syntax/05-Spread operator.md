# JavaScript Spread Operator

## Introduction to the JavaScript spread operator

ES6 提供了一个新的运算符，称为展开运算符，它由三个点 (...) 组成。展开运算符扩展可迭代对象（例如数组、映射或集合）的元素。

```js
const odd = [1,3,5];
const combined = [2,4,6, ...odd];
console.log(combined); // [ 2, 4, 6, 1, 3, 5 ]
```

位于奇数数组前面的三个点 (...) 是展开运算符。展开运算符 (...) 解包（unpack）奇数数组的元素。

> ES6 还具有三个点 (...)，这是一个 rest parameter，它将函数的所有剩余参数收集到一个数组中。

```js
function f(a, b, ...args) {
	console.log(args);
}

f(1, 2, 3, 4, 5); // [ 3, 4, 5 ]
```

因此，三个点 (...) 同时表示 spread operator 和 rest parameter。

主要区别：

- spread operator 解包**可迭代对象（iterable object）**的元素。
- rest parameter 将元素打包到数组中。

rest parameter 必须是函数的最后一个参数。然而，扩展运算符可以在任何地方：

```js
const odd = [1,3,5];
const combined = [...odd, 2,4,6];
console.log(combined); // [ 1, 3, 5, 2, 4, 6 ]

const odd = [1,3,5];
const combined = [2,...odd, 4, 6];
console.log(combined); // [2, 1, 3, 5, 4, 6]
```

> ES2018 将 spead operator 扩展到对象，这称为 object spread。

## JavaScript spread operator and apply() method

```js
function compare(a, b) {
    return a - b;
}
```

在 ES5 中，要将两个数字的数组传递给 compare() 函数，通常使用 apply() 方法，因为 apply() 方法的参数传递是以数组的形式并自动解包的。

```js
let result = compare.apply(null, [1, 2]);
console.log(result); // -1
```

但是，通过使用扩展运算符，可以将两个数字的数组传递给compare()函数：

```js
let result = compare(...[1, 2]);
console.log(result); // -1
```

展开运算符展开数组的元素。

## A better way to use the Array’s push() method example

数组对象的 push() 方法向数组添加一个或多个元素。如果要将数组传递给 push() 方法，则需要使用 apply() 方法：

```js
let rivers = ['Nile', 'Ganges', 'Yangte'];
let moreRivers = ['Danube', 'Amazon'];

[].push.apply(rivers, moreRivers);
console.log(rivers); // [ 'Nile', 'Ganges', 'Yangte', 'Danube', 'Amazon' ]
```

使用扩展运算符来提高代码的可读性：

```js
rivers.push(...moreRivers);
```

## JavaScript spread operator and array manipulation

### Constructing array literal

```js
let initialChars = ['A', 'B'];
let chars = [...initialChars, 'C', 'D'];
console.log(chars); // ["A", "B", "C", "D"]
```

### Concatenating arrays

```js
let numbers = [1, 2];
let moreNumbers = [3, 4];
let allNumbers = [...numbers, ...moreNumbers];
console.log(allNumbers); // [1, 2, 3, 4]
```

### Copying an array

```js
let scores = [80, 70, 90];
let copiedScores = [...scores];
console.log(copiedScores); // [80, 70, 90]
```

### JavaScript spread operator and strings

```js
let chars = ['A', ...'BC', 'D'];
console.log(chars); // ["A", "B", "C", "D"]
```











































