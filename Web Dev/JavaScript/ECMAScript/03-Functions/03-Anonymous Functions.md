# JavaScript Anonymous Functions

## Introduction to JavaScript anonymous functions

匿名函数是没有名称的函数。下面展示了如何定义匿名函数：

```js
(function () {
   //...
});
```

请注意，如果不将匿名函数放在括号 () 内，则会出现语法错误。括号 () 使匿名函数成为返回函数对象的表达式。

匿名函数在初始创建后不可访问。因此，经常需要将其分配给变量。

```js
let show = function() {
    console.log('Anonymous function');
};

show();
```

因为后面需要调用匿名函数，所以我们将匿名函数赋值给show变量。

由于匿名函数对 show 变量的整个赋值构成了一个有效的表达式，因此不需要将匿名函数括在括号 () 内。

## Using anonymous functions as arguments

在实践中，经常将匿名函数作为参数传递给其他函数。

```js
setTimeout(function() {
    console.log('Execute later after 1 second')
}, 1000);
```

> 请注意，函数是 JavaScript 中的一等公民。因此，可以将一个函数作为参数传递给另一个函数。

## Immediately invoked function execution-IIFE

如果想创建一个函数并在声明后立即执行它，可以像这样声明一个匿名函数：

```js
(function() {
    console.log('IIFE');
})();
// IIFE
```

首先，定义一个函数表达式：

```js
(function () {
    console.log('Immediately invoked function execution');
})
```

该表达式返回一个函数。

其次，通过添加尾括号 () 来调用该函数：

```js
(function () {
    console.log('Immediately invoked function execution');
})();
```

有时，可能希望将参数传递给匿名函数，如下所示：

```js
let person = {
    firstName: 'John',
    lastName: 'Doe'
};

(function () {
    console.log(person.firstName + ' ' + person.lastName);
})(person);
// John Doe
```

## Arrow functions

ES6 引入了箭头函数表达式，为声明匿名函数提供了简写。
