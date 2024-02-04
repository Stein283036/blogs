# JavaScript call() Method

## Introduction to the JavaScript call() method

在 JavaScript 中，函数是 Function 类型的实例。例如：

```js
function add(x, y) {
  return x + y;
}

console.log(add instanceof Function); // true
```

Function.prototype 类型具有 call() 方法，其语法如下：

```js
functionName.call(thisArg, arg1, arg2, ...);
```

在此语法中，call() 方法使用参数（arg1、arg2、...）调用函数 functionName，并将 this 设置为函数内的 thisArg 对象。

- thisArg 是函数 functionName 中 this 对象引用的对象。
- arg1、arg2、.. 是传递到 functionName 的函数参数。

call() 方法返回调用 functionName() 的结果。

以下示例定义了 add() 函数并正常调用它：

```js
function add(x, y) {
  return x + y;
}

let result = add(10, 20);
console.log(result); // 30
```

以下代码调用 add() 函数，但使用 call() 方法：

默认情况下，函数内的 this 设置为全局对象，即 Web 浏览器中的 window 和 Node.js 中的 global。

> 请注意，在严格模式下，函数内的 this 设置为 undefined，而不是全局对象。

考虑以下示例：

```js
var greeting = 'Hi';

var messenger = {
    greeting: 'Hello'
}

function say(name) {
    console.log(this.greeting + ' ' + name);
}
```

在 say() 函数中，我们通过 this 值引用 greeting。如果只是通过 call() 方法调用 say() 函数，如下所示：

```js
say.call(this,'John');
```

它将向控制台显示以下输出，因为此时 this 指向的是全局对象：

```js
"Hi John"
```

但是，当您调用 say 函数对象的 call() 方法并将 messenger 对象作为 this 值传递时：

```js
say.call(messenger,'John');
```

输出将是：

```js
"Hello John"
```

在这种情况下，say() 函数中的 this 值引用 messenger 对象，而不是全局对象。

## Using the JavaScript call() method to chain constructors for an object

可以使用 call() 方法来链接对象的构造函数。考虑以下示例：

```js
function Box(height, width) {
  this.height = height;
  this.width = width;
}

function Widget(height, width, color) {
  Box.call(this, height, width);
  this.color = color;
}

let widget = new Widget('red', 100, 200);

console.log(widget); // Widget { height: 'red', width: 100, color: 200 }
```

## Using the JavaScript call() method for function borrowing

以下示例说明了如何使用 call() 方法来借用函数：

```js
const car = {
  name: 'car',
  start() {
    console.log('Start the ' + this.name);
  },
  speedUp() {
    console.log('Speed up the ' + this.name);
  },
  stop() {
    console.log('Stop the ' + this.name);
  },
};

const aircraft = {
  name: 'aircraft',
  fly() {
    console.log('Fly');
  },
};

car.start.call(aircraft);
car.speedUp.call(aircraft);
aircraft.fly();

// 输出
Start the aircraft
Speed up the aircraft
Fly
```

在 start() 和 speedUp() 方法中， this 引用了 aircraft 对象，而不是 car 对象。

下面的示例说明了arguments对象如何通过call()函数借用Array.prototype的filter()方法：

```js
function isOdd(number) {
  return number % 2 !== 0;
}

function getOddNumbers() {
  return Array.prototype.filter.call(arguments, isOdd);
}

let results = getOddNumbers(10, 1, 3, 4, 8, 9);
console.log(results); // [ 1, 3, 9 ]
```

首先，定义 isOdd() 函数，如果数字是奇数，则该函数返回 true：

```js
function isOdd(number) {
  return number % 2 !== 0;
}
```

其次，定义 getOddNumbers() 函数，该函数接受任意数量的参数并返回仅包含奇数的数组：

```js
function getOddNumbers() {
  // 因为 arguments 是一个 array-like，所以不能调用 Array.prototype 对象中定义的 filter 等数组方法
  return Array.prototype.filter.call(arguments, isOdd);
}
```

在此示例中，arguments 对象借用了 Array.prototype 对象的 filter() 方法。

第三，调用 getOddNumbers() 函数：

```js
let results = getOddNumbers(10, 1, 3, 4, 8, 9);
console.log(results);
```