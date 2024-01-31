# JavaScript Closures

## Introduction to JavaScript closures

在 JavaScript 中，闭包（closure）是一个从其内部作用域引用外部作用域中的变量的**函数**。闭包将外部作用域保留在其内部作用域内。

要理解闭包，需要首先了解词法作用域（lexical scoping）如何工作。

### Lexical scoping

词法作用域通过源代码中声明的变量的位置来定义变量的作用域。例如：

```js
let name = 'John';

function greeting() { 
    var message = 'Hi';
    console.log(message + ' '+ name);
}
```

在这个例子中：

- 变量 name 是全局变量（global scope）。它可以从任何地方访问，包括在greeting()函数中。
- 变量 message 是一个局部变量（function scope），只能在greeting() 函数中访问。

如果尝试在greeting()函数之外访问message变量，将收到错误。

因此 JavaScript 引擎使用作用域来管理变量的可访问性。

根据词法作用域，作用域可以嵌套，内部函数可以访问其外部作用域中声明的变量。例如：

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

sayHi() 是内部函数，仅在greeting() 函数体内可用。

sayHi() 函数可以访问外部函数的变量，例如greeting() 函数的 message 变量。

在greeting()函数中，我们调用sayHi()函数来显示消息Hi。

### JavaScript closures

让我们修改greeting()函数：

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

现在，greeting() 函数返回 sayHi() 函数对象，而不是在greeting() 函数内执行 sayHi() 函数。

请注意，函数是 JavaScript 中的一等公民，因此，可以从另一个函数返回一个函数。

在greeting()函数之外，我们将greeting()函数返回的值分配给hi变量，该值是对sayHi()函数的引用。

然后我们使用该函数的引用执行 sayHi() 函数：hi()。如果运行代码，将得到与上面相同的效果。

然而，有趣的是，通常局部变量仅在函数执行期间存在。

这意味着当greeting()函数执行完毕后，message变量将不再可访问。

在这种情况下，我们执行引用 sayHi() 函数的 hi() 函数，消息变量仍然存在。

其神奇之处在于封闭。换句话说，sayHi() 函数是一个闭包。

闭包是一个将外部作用域保留在其内部作用域中的函数。

### More JavaScript Closure examples

下面的例子说明了一个更实际的闭包示例。

```js
function greeting(message) {
   return function(name){
        return message + ' ' + name;
   }
}
let sayHi = greeting('Hi');
let sayHello = greeting('Hello');

console.log(sayHi('John')); // Hi John
console.log(sayHello('John')); // Hello John
```

