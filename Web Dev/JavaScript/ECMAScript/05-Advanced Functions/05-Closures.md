# JavaScript Closures

## Introduction to JavaScript closures

在 JavaScript 中，闭包（closure）是一个从其内部作用域引用外部作用域中的变量的**函数**。闭包将外部作用域保留在其内部作用域内。

要理解闭包，需要首先了解词法作用域（lexical scoping）如何工作。

### Lexical scoping

词法作用域通过源代码中声明的变量的位置来定义变量的作用域。

```js
let name = 'John';

function greeting() { 
    var message = 'Hi';
    console.log(message + ' '+ name);
}
```

在这个例子中：

- 变量 name 是全局变量（global scope）。它可以从任何地方访问，包括在 greeting() 函数中。
- 变量 message 是一个局部变量（function scope），只能在 greeting() 函数中访问。

如果尝试在 greeting() 函数之外访问 message 变量，将收到错误。

因此 JavaScript 引擎使用作用域来管理变量的可访问性。

根据词法作用域，作用域可以嵌套，内部函数可以访问其外部作用域中声明的变量。

```js
function greeting() {
    let message = 'Hi';

    function sayHi() {
        console.log(message);
    }

    sayHi();
}

greeting();
```

greeting() 函数创建一个名为 message 的局部变量和一个名为 sayHi() 的函数。

sayHi() 是内部函数，仅在 greeting() 函数体内可用。

sayHi() 函数可以访问外部函数的变量，例如 greeting() 函数的 message 变量。

在 greeting() 函数中，我们调用 sayHi() 函数来显示 message 变量的值 Hi。

### JavaScript closures

让我们修改 greeting() 函数：

```js
function greeting() {
    let message = 'Hi';

    function sayHi() {
        console.log(message);
    }

    return sayHi;
}
let hi = greeting();
hi(); // still can access the message variable
```

现在，greeting() 函数返回 sayHi() 函数对象，而不是在 greeting() 函数内执行 sayHi() 函数。

在 greeting() 函数之外，我们将 greeting() 函数返回的值分配给 hi 变量，该值是对 sayHi() 函数的引用。

然后我们使用该函数的引用执行 sayHi() 函数：hi()。

然而，有趣的是，通常局部变量仅在函数执行期间存在。

这意味着当 greeting() 函数执行完毕后，message 变量将不再可访问。

在这种情况下，我们执行引用 sayHi() 函数的 hi() 函数，message 变量仍然存在。

其神奇之处在于封闭。换句话说，sayHi() 函数是一个闭包。

闭包是一个将外部作用域保留在其内部作用域中的函数。

### More JavaScript Closure examples

```js
function greeting(message) {
   return function(name){ // 匿名函数
        return message + ' ' + name;
   }
}
let sayHi = greeting('Hi');
let sayHello = greeting('Hello');

console.log(sayHi('John')); // Hi John
console.log(sayHello('John')); // Hello John
```

greeting() 函数接受一个名为 message 的参数，并返回一个接受名为 name 的单个参数的函数。

return 函数返回一条问候消息，该消息是 message 和 name 变量的组合。

greeting() 函数的行为类似于函数工厂。它使用各自的消息 Hi 和 Hello 创建 sayHi() 和 sayHello() 函数。

sayHi() 和 sayHello() 是闭包。它们共享相同的函数体，但存储不同的作用域。

在 sayHi() 闭包中，message 是 Hi，而在 sayHello() 闭包中，message 是 Hello。

## JavaScript closures in a loop

```js
for (var index = 1; index <= 3; index++) {
    setTimeout(function () {
        console.log('after ' + index + ' second(s):' + index);
    }, index * 1000);
}

// 输出
after 4 second(s):4
after 4 second(s):4
after 4 second(s):4
```

该代码显示了相同的消息。

我们想要在循环中做的是在每次迭代时复制 index 的值，以便在 1、2 和 3 秒后显示消息。

4 秒后看到相同消息的原因是回调传递给 setTimeout() 一个闭包。它会记住上次循环迭代中 index 的值，即 4。

此外，for 循环创建的所有三个闭包共享相同的全局范围，访问相同的 index 值。

要解决此问题，需要在循环的每次迭代中创建一个新的闭包作用域。

有两种流行的解决方案：IIFE 和 let 关键字。

### Using the IIFE solution

在此解决方案中，使用 IIFE(immediately invoked function expression)，因为 **IIFE 通过声明函数并立即执行它来创建新作用域**。

```js
for (var index = 1; index <= 3; index++) {
    (function (index) {
        setTimeout(function () {
            console.log('after ' + index + ' second(s):' + index);
        }, index * 1000);
    })(index);
}

// 输出
after 1 second(s):1
after 2 second(s):2
after 3 second(s):3
```

### Using let keyword in ES6

在 ES6 中，可以使用 let 关键字来声明块作用域的变量。

如果在 for 循环中使用 let 关键字，它将在每次迭代中创建一个新的词法范围。换句话说，每次迭代都会有一个新的索引变量。

```js
for (let index = 1; index <= 3; index++) {
    setTimeout(function () {
        console.log('after ' + index + ' second(s):' + index);
    }, index * 1000);
}

// 输出
after 1 second(s):1
after 2 second(s):2
after 3 second(s):3
```