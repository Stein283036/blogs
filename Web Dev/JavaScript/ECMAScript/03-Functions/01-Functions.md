# JavaScript Functions

## Introduction to JavaScript functions

为了避免在各处重复相同的代码，可以使用函数来包装该代码并重用它。

JavaScript 提供了许多内置函数，例如 parseInt() 和 parseFloat()。

## Declare a function

要声明函数，请使用 function 关键字，后跟函数名称、参数列表和函数体，如下所示：

```js
function functionName(parameters) {
    // function body
    // ...
}
```

按照惯例，函数名称采用驼峰式命名法，并以 getData()、fetchContents() 和 isValid() 等动词开头。

函数可以接受零个、一个或多个参数。当有多个参数时，需要使用逗号分隔两个参数。

## Calling a function

要使用函数，需要调用它。调用函数也称为调用函数。要调用函数，可以使用其名称，后跟括在括号中的实参：

```js
functionName(arguments);
```

### Parameters vs. Arguments

术语 parameters 和 arguments 通常可以互换使用。然而，它们本质上是不同的。

声明函数时，指定形参。但是，在调用函数时，传递与形参相对应的实参。

## Returning a value

JavaScript 中的每个函数都会隐式返回 undefined，除非显式指定返回值。

```js
function say(message) {
    console.log(message);
}

let result = say('Hello');
console.log('Result:', result);
// 输出
Hello
Result: undefined
```

要指定函数的返回值，使用 return 语句，后跟表达式或值：

```js
return expression;
```

## The arguments object

在函数内部，可以访问称为 arguments 的对象，该对象表示函数的命名参数。

arguments 对象的行为类似于数组，尽管它不是 Array 类型的实例。

例如，可以使用方括号 [] 访问 arguments：arguments[0] 返回第一个参数，arguments[1] 返回第二个参数，依此类推。

可以使用 arguments 对象的 length 属性来确定参数的数量。

## Function hoisting

JavaScript 中的提升（Hoisting）是指在代码执行过程中，JavaScript 引擎会将变量声明（var）、函数声明（function）提升到其作用域的顶部，但是只是提升声明本身，而不是初始化或赋值。

函数声明和类声明之间的一个重要区别在于，函数声明会提升，类声明不会。你首先需要声明你的类，然后再访问它。

只有变量声明、函数声明会被提升，而变量赋值、函数表达式（如匿名函数表达式、箭头函数表达式）不会被提升。

在 JavaScript 中，可以在声明函数之前使用它。

```js
showMe(); // a hoisting example

function showMe(){
    console.log('an hoisting example');
}
```

此功能称为提升。函数提升是 JavaScript 引擎在执行函数声明之前将函数声明物理移动到代码顶部的一种机制。
