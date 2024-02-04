# JavaScript Hoisting

## Introduction to the JavaScript hoisting

当 JavaScript 引擎执行 JavaScript 代码时，它会创建全局执行上下文。全局执行上下文有两个阶段：

- Creation Phase
- Execution Phase

在 **Creation Phase**，JavaScript 引擎将变量和函数声明移动到代码的顶部。这在 JavaScript 中称为提升。

## Variable hoisting

Variable hoisting means the JavaScript engine moves the variable declarations to the top of the script. For example, the following example declares the counter variable and initialize its value to 1:

```js
console.log(counter); // 👉 undefined
var counter = 1;
```

但是，第一行代码不会导致错误。原因是 JavaScript 引擎将变量声明移至脚本的顶部。

Technically, the code looks like the following in the execution phase:

```js
var counter;

console.log(counter); // 👉 undefined
counter = 1;
```

During the creation phase of the global execution context, the JavaScript engine places the variable `counter` in the memory and initializes its value to `undefined`.

### The let keyword

下面使用 let 关键字声明变量 counter：

```js
console.log(counter);
let counter = 1;
```

JavaScript 发出以下错误：

```js
"ReferenceError: Cannot access 'counter' before initialization
```

The error message explains that the `counter` variable is already in the heap memory. However, it hasn’t been initialized.

Behind the scenes, the JavaScript engine **hoists** the variable declarations that use the `let` keyword. However, it doesn’t initialize the `let` variables.

Notice that if you access a variable that doesn’t exist, the JavaScript will throw a different error:

```js
console.log(alien);
let counter = 1;
"ReferenceError: alien is not defined
```

## Function hoisting

Like variables, the JavaScript engine also hoists the function declarations. This means that the JavaScript engine also moves the function declarations to the top of the script. For example:

```js
let x = 20,
  y = 10;

let result = add(x, y); 
console.log(result); // 👉 30

function add(a, b) {
  return a + b;
}
```

在此示例中，在函数定义之前调用了 add() 函数。上面的代码相当于下面的代码：

```js
function add(a, b){
    return a + b;
}

let x = 20,
    y = 10;

let result = add(x,y);
console.log(result); // 👉 30
```

在执行上下文的创建阶段，JavaScript 引擎将 add() 函数声明放置在堆内存中。准确地说，JavaScript 引擎创建一个 Function 类型的对象和一个引用该函数对象的函数引用 add。

### Function expressions

```js
let x = 20,
    y = 10;

let result = add(x,y); // Uncaught ReferenceError: Cannot access 'add' before initialization
console.log(result);

let add = function(x, y) {
    return x + y;
}
```

执行该代码，会出现以下错误：

```js
Uncaught ReferenceError: Cannot access 'add' before initialization
```

在全局执行上下文的创建阶段，JavaScript 引擎在内存中创建 add 变量并提升，但是不会为其初始化为 undefined，因此该变量会暂时性死区。

### Arrow functions

以下示例将 add 函数表达式更改为箭头函数：

```js
let x = 20,
    y = 10;

let result = add(x,y); // Uncaught TypeError: add is not a function
console.log(result);

var add = (x, y) => x + y; 
```

这里使用 var 声明变量 add，该代码发出与函数表达式示例相同的错误，因为箭头函数是定义函数表达式的语法糖。

与函数表达式类似，箭头函数不会提升。

## Class hoisting

### Class declaration

```js
let instance = new MyClass(); // 正常执行
class MyClass {}
```

### Class expression

```js
let instance = new MyClass(); // 抛出错误：TypeError: MyClass is not a constructor
var MyClass = class {};
```
