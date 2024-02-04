# JavaScript let: Declaring Block-Scoped Variables

## Introduction to the JavaScript let keyword

在 ES5 中，当使用 var 关键字声明变量时，该变量的作用域是全局的或局部（函数作用域）的。如果在函数外部声明变量，则该变量的作用域是全局的。当在函数内声明变量时，该变量的作用域是局部的。

ES6 提供了一种使用 let 关键字声明变量的新方法。 let 关键字与 var 关键字类似，只不过这些变量是块作用域（block-scoped）的。

```js
let variable_name;
```

在 JavaScript 中，块由 {} 表示，例如 if else、for、do while、while、try catch 等：

```js
if(condition) {
   // inside a block
}
```

```js
let x = 10;
if (x == 10) {
    let x = 20;
    console.log(x); // 20:  reference x inside the block
}
console.log(x); // 10: reference at the begining of the script
```

## JavaScript let and global object

当使用 var 关键字声明全局变量时，该变量被添加到全局对象的属性列表中。对于 Web 浏览器，全局对象是 window。

```js
var a = 10;
console.log(window.a); // 10
```

但是，当使用 let 关键字声明变量时，该变量不会作为属性附加到全局对象。

```js
let b = 20;
console.log(window.b); // undefined
```

## JavaScript let and callback function in a for loop

```js
for (var i = 0; i < 5; i++) {
    setTimeout(function () {
        console.log(i);
    }, 1000);
}
```

该代码的目的是每秒向控制台输出从 0 到 4 的数字。但是，它输出数字 5 五次：

在此示例中，变量 i 是全局变量。循环结束后，其值为 5。当回调函数传递给 setTimeout() 函数执行时，它们引用值为 5 的同一变量 i。

在 ES5 中，可以通过创建另一个作用域来解决此问题，以便每个回调函数引用一个新变量。要创建新作用域，需要创建一个函数。通常，可以按如下方式使用 IIFE 模式：

```js
for (var i = 0; i < 5; i++) {
    (function (j) {
        setTimeout(function () {
            console.log(j);
        }, 1000);
    })(i);
}
```

在 ES6 中，let 关键字在每次循环迭代中声明一个新变量。因此，只需将 var 关键字替换为 let 关键字即可解决该问题：

```js
for (let i = 0; i < 5; i++) {
    setTimeout(function () {
        console.log(i);
    }, 1000);
}
```

为了让代码完全符合ES6风格，可以使用箭头函数：

```js
for (let i = 0; i < 5; i++) {
    setTimeout(() => console.log(i), 1000);
}
```

## Redeclaration

var 关键字允许重新声明变量而不会出现任何问题：

```js
var counter = 0;
var counter;
console.log(counter); // 0
```

但是，使用 let 关键字重新声明变量将导致错误：

```js
let counter = 0;
let counter;
console.log(counter);
Uncaught SyntaxError: Identifier 'counter' has already been declared
```

## JavaScript let variables and hoisting

```js
{
    console.log(counter); // 
    let counter = 10;    
}
Uncaught ReferenceError: Cannot access 'counter' before initialization
```

In this example, accessing the `counter` variable before declaring it causes a `ReferenceError`. You may think that a variable declaration using the `let` keyword does not **hoist,** but it does.

事实上，JavaScript 引擎会将 let 关键字声明的变量提升到块的顶部。但是，JavaScript 引擎不会初始化该变量。因此，当你引用一个未初始化的变量时，你会得到一个 ReferenceError。

## Temporal death zone (TDZ)

由 let 关键字声明的变量有一个所谓的临时死区 (TDZ)。 TDZ 是从块开始到处理变量声明的时间。

The following example illustrates that the temporal dead zone is time-based, not location-based*.*

```js
{ // enter new scope, TDZ starts
    let log = function () {
        console.log(message); // message declared later
    };

    // This is the TDZ and accessing log
    // would cause a ReferenceError

    let message = 'Hello'; // TDZ ends
    log(); // called outside TDZ
}
```

首先，{} 开始一个新的块作用域，因此，TDZ 开始。

其次，log() 函数表达式访问 message 变量。然而，log() 函数还没有被执行。

第三，声明 message 变量并将其值初始化为“Hello”。从块作用域开始到访问 message 变量的时间称为 TDZ。当 JavaScript 引擎处理完该声明时，TDZ 结束。

最后，调用 log() 函数来访问 TDZ 之外的 message 变量。

如果访问 TDZ 中由 let 关键字声明的变量，将得到一个 ReferenceError：

```js
{ // TDZ starts
    console.log(typeof myVar); // undefined
    console.log(typeof message); // ReferenceError
    let message; // TDZ ends
}
```

myVar 变量是一个不存在的变量，因此，其类型是 undefined。

TDZ 可防止在声明之前意外引用变量。