# ES6 Destructuring Assignment

ES6 提供了一个称为解构赋值的新功能，将对象的属性或数组的元素解构为单独的变量。

## Introduction to JavaScript Array destructuring

有一个返回数字数组的函数：

```js
function getScores() {
   return [70, 80, 90];
}
```

以下代码调用 getScores() 函数并将返回值分配给变量：

```js
let scores = getScores();
```

为了获取每一个单独的 score，需要使用数组的索引（属性）访问元素：

```js
let x = scores[0], 
    y = scores[1], 
    z = scores[2];
```

在 ES6 之前，没有直接的方法将返回数组的元素分配给多个变量。

从 ES6 开始，可以使用解构赋值：

```js
let [x, y, z] = getScores();

console.log(x); // 70
console.log(y); // 80
console.log(z); // 90
```

如果 getScores() 函数返回一个包含两个元素的数组，则第三个变量将是 undefined：

```js
function getScores() {
   return [70, 80];
}

let [x, y, z] = getScores();

console.log(x); // 70
console.log(y); // 80
console.log(z); // undefined
```

如果 getScores() 函数返回一个包含三个以上元素的数组，则其余元素将被丢弃：

```js
function getScores() {
   return [70, 80, 90, 100];
}

let [x, y, z] = getScores();

console.log(x); // 70
console.log(y); // 80
console.log(z); // 90
```

## Array Destructuring Assignment and Rest syntax

可以使用 rest parameter (...) 获取数组的所有剩余元素并将它们放入新数组中：

```js
let [x, y, ...args] = getScores();
console.log(x); // 70
console.log(y); // 80
console.log(args); // [90, 100]
```

## Setting default values

```js
function getItems() {
    return [10, 20];
}

let [, , z = 30] = getItems();
console.log(z); // 30
```

如果 getItems() 函数不返回数组，则解构赋值将导致错误：

```js
function getItems() {
    return null;
}

let [x = 1, y = 2] = getItems();
Uncaught TypeError: getItems is not a function or its return value is not iterable
```

解决方法：

```js
function getItems() {
    return null;
}

let [a = 10, b = 20] = getItems() || [];

console.log(a); // 10
console.log(b); // 20
```

## Nested array destructuring

以下函数返回一个数组，其中包含嵌套数组的元素：

```js
function getProfile() {
    return [
        'John',
        'Doe',
        ['Red', 'Green', 'Blue']
    ];
}
```

由于返回数组的第三个元素是另一个数组，因此需要使用嵌套数组解构语法对其进行解构：

```js
function getProfile() {
  return ['John', 'Doe', ['Red', 'Green', 'Blue']]
}

let [firstName, lastName, [red, green, blue]] = getProfile()
console.log(firstName, lastName, red, green, blue) // John Doe Red Green Blue
```

## Array Destructuring Assignment Applications

### Swapping variables

```js
let a = 10, 
    b = 20;

[a, b] = [b, a];

console.log(a); // 20
console.log(b); // 10
```

### Functions that return multiple values

在 JavaScript 中，函数只可以 return 一个值（primitive 或者 object）。但是，可以返回包含多个值的数组：

```js
function stat(a, b) {
    return [
        a + b,
        (a + b) / 2,
        a - b
    ]
}
```

然后使用数组解构赋值语法将返回数组的元素解构为变量：

```js
let [sum, average, difference] = stat(20, 10);
console.log(sum, average, difference); // 30, 15, 10
```