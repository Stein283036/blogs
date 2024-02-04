# An Introduction to JavaScript Arrow Functions

## Introduction to JavaScript arrow functions

ES6 箭头函数提供了一种替代方法来编写比函数表达式更短的语法。

以下示例定义一个返回两个数字之和的函数表达式：

```js
let add = function (x, y) {
	return x + y;
};

console.log(add(10, 20)); // 30
```

以下示例等效于上面的 add() 函数表达式，但使用箭头函数代替：

```js
let add = (x, y) => x + y;
console.log(add(10, 20)); // 30;
```

在此示例中，箭头函数有一个表达式 x + y，因此它返回该表达式的结果。

但是，如果使用块语法 {}，则需要指定 return 关键字：

```js
let add = (x, y) => { return x + y; };
```

typeof 运算符返回指示箭头函数类型为 function。

```js
console.log(typeof add); // function
```

箭头函数也是 Function 类型的实例，如下例所示：

```js
console.log(add instanceof Function); // true
```

### JavaScript arrow functions with multiple parameters

如果箭头函数有两个或多个参数，则使用以下语法：

```js
(p1, p2, ..., pn) => expression;
```

例如，要按降序对数字数组进行排序，可以使用数组对象的 sort() 方法，如下所示：

```js
let numbers = [4,2,6];
numbers.sort(function(a,b){ 
    return b - a; 
});
console.log(numbers); // [6,4,2]
```

使用箭头函数语法，代码更加简洁：

```js
let numbers = [4,2,6];
numbers.sort((a,b) => b - a);
console.log(numbers); // [6,4,2]
```

### JavaScript arrow functions with a single parameter

如果箭头函数采用单个参数，则使用以下语法：

```js
(p1) => { statements }
```

注意，您可以省略括号，如下所示：

```js
p => { statements }
```

以下示例使用箭头函数作为 map() 方法的参数，该方法将字符串数组转换为字符串长度数组。

```js
let names = ['John', 'Mac', 'Peter'];
let lengths = names.map(name => name.length);

console.log(lengths); // [ 4, 3, 5 ]
```

### JavaScript arrow functions with no parameter

如果箭头函数没有参数，则必须需要使用括号，如下所示：

```js
() => { statements }
```

例如：

```js
let logDoc = () => console.log(window.document);
logDoc();
```

## Statements & expressions in the arrow function body

在 JavaScript 中，表达式的计算结果为如下例所示的值。

```js
10 + 20;
```

语句执行特定任务，例如：

```js
if (x === y) {
    console.log('x equals y');
}
```

如果在箭头函数体中使用一个表达式，则不需要使用 {}。

```js
let square = x => x * x;
```

但是，如果使用一条语句，则必须将其括在一对大括号内，如下例所示：

```js
let except = msg => {
    throw msg;
};
```

## JavaScript arrow functions and object literal

考虑以下示例：

```js
let setColor = function (color) {
    return {value: color}
};

let backgroundColor = setColor('Red');
console.log(backgroundColor.value); // "Red"
```

setColor() 函数表达式返回一个对象，该对象的 value 属性设置为 color 参数。

如果使用以下语法从箭头函数返回对象字面量，将不会起作用。

```js
p => {object:literal}
```

例如：

```js
let setColor = color => {value: color };
```

由于块和对象字面量都使用大括号，因此 JavaScript 引擎无法区分块和对象。

要解决此问题，需要将对象字面量括在括号中，如下所示：

```js
let setColor = color => ({value: color });
```

## Arrow function vs. regular function

箭头函数和常规函数之间有两个主要区别。

- 首先，在箭头函数中，this、arguments、super、new.target 是词法的。这意味着箭头函数使用封闭词法范围（enclosing lexical scope）中的这些变量。
- 其次，箭头函数不能用作函数构造器。如果使用 new 关键字从箭头函数创建新对象，将收到错误。

### JavaScript arrow functions and `this` value

在 JavaScript 中，一个新函数定义了自己的 this 值。然而，箭头函数的情况并非如此。例如：

```js
function Car() {
    this.speed = 0;
    this.speedUp = function (speed) {
        this.speed = speed;
        setTimeout(function () {
            console.log(this.speed); // undefined
        }, 1000);
    };
}
let car = new Car();
car.speedUp(50);
```

在setTimeout()函数的匿名函数中，this.speed是 undefined。原因是匿名函数的 this 遮盖了 speedUp() 方法的 this，因为匿名函数中的 this 指向全局对象。

要解决此问题，可以将 this 值分配给一个不在匿名函数内部隐藏的变量，如下所示：

```js
function Car() {
    this.speed = 0;
    this.speedUp = function (speed) {
        this.speed = speed;
        let self = this;
        setTimeout(function () {
            console.log(self.speed);
        }, 1000);
    };
}
let car = new Car();
car.speedUp(50); // 50;
```

与匿名函数不同，箭头函数捕获封闭上下文（enclosing context）的 this 值，而不是创建自己的 this 上下文。以下代码应该按预期工作：

```js
function Car() {
    this.speed = 0;
    this.speedUp = function (speed) {
        this.speed = speed;
        setTimeout(
            () => console.log(this.speed),
            1000);
    };
}
let car = new Car();
car.speedUp(50); // 50;
```

### JavaScript arrow functions and the arguments object

箭头函数没有 arguments 对象。例如：

```js
function show() {
    return x => x + arguments[0];
}

let display = show(10, 20);
let result = display(5);
console.log(result); // 15
```

showMe() 函数内的箭头函数引用arguments 对象。然而，这个arguments对象属于show()函数，而不是箭头函数。

此外，箭头函数没有 new.target 关键字。

### JavaScript arrow functions and the prototype property

当使用 function 关键字定义函数时，该函数有一个称为原型的属性：

```js
function dump( message ) {
    console.log(message);
}
console.log(dump.hasOwnProperty('prototype')); // true
```

然而，箭头函数没有原型属性：

```js
let dump = message => console.log(message);
console.log(dump.hasOwnProperty('prototype')); // false
```

使用箭头函数进行回调和闭包是一种很好的做法，因为箭头函数的语法更清晰。



















































