# JavaScript Default Parameters

在 JavaScript 中，如果没有值或 `undefined` 传递到函数中，默认函数参数允许使用默认值初始化命名参数。

## Setting JavaScript default parameters for a function

在 JavaScript 中，参数的默认值是 `undefined`。这意味着，如果不将参数传递给函数，则其参数的默认值将是 undefined。

假设要为 message 参数指定默认值 'Hi'。

实现此目的的典型方法是使用三元运算符测试参数值并分配默认值（如果未定义）：

```js
function say(message) {
    message = typeof message !== 'undefined' ? message : 'Hi';
    console.log(message);
}
say(); // 'Hi'
```

ES6 提供了一种更简单的方法来设置函数参数的默认值，如下所示：

```js
function fn(param1=default1, param2=default2,..) {
}
```

在上面的语法中，可以使用赋值运算符 (=) 和参数名称后面的默认值来设置该参数的默认值。

```js
function say(message='Hi') {
    console.log(message);
}

say(); // 'Hi'
say(undefined); // 'Hi'
say('Hello'); // 'Hello'
```

### Using functions

可以使用函数的返回值作为参数的默认值。

```js
let taxRate = () => 0.1;
let getPrice = function( price, tax = price * taxRate() ) {
    return price + tax;
}

let fullPrice = getPrice(100);
console.log(fullPrice); // 110
```

### The arguments object

函数内 arguments 对象的值是传递给函数的实际参数的数量。

```js
function add(x, y = 1, z = 2) {
    console.log( arguments.length );
    return x + y + z;
}

add(10); // 1
add(10, 20); // 2
add(10, 20, 30); // 3
```
