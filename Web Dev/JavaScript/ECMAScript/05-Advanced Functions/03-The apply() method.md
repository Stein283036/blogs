# JavaScript apply() method

## Introduction to the JavaScript `apply()` method

Function.prototype.apply() 方法允许使用给定的 this 值和以数组形式提供的参数来调用函数。

```js
fn.apply(thisArg, [args]);
```

apply() 方法接受两个参数：

- thisArg 是为调用函数 fn 提供的 this 值。
- args 参数是一个数组，指定函数 fn 的参数。从 ES5 开始，args 参数可以是类数组对象或数组对象。

apply() 方法与 call() 方法类似，只不过它将函数的参数作为数组而不是单个参数。

## JavaScript a`pply()` method examples

### Simple JavaScript `apply()` method example

假设有一个 person 对象：

```js
const person = {
    firstName: 'John',
    lastName: 'Doe'
}
```

以及一个名为greet()的函数，如下所示：

```js
function greet(greeting, message) {
    return `${greeting} ${this.firstName}. ${message}`;
}
```

greet() 函数接受两个参数：greeting 和 message。在greet()函数中，我们引用了一个具有firstName属性的对象。

以下示例演示如何使用 apply() 方法调用greet() 函数，并将 this 设置为 person 对象：

```js
let result = greet.apply(person, ['Hello', 'How are you?']);

console.log(result); // Hello John. How are you?
```

apply() 方法调用 greet() 函数，并将 this 值设置为 person 对象，并将参数设置为数组 ['Hello', 'How are you?']。

### Function borrowing

apply() 方法允许一个对象借用另一个对象的方法，而无需重复代码。

假设有以下计算机对象：

```js
const computer = {
    name: 'MacBook',
    isOn: false,
    turnOn() {
        this.isOn = true;
        return `The ${this.name} is On`;
    },
    turnOff() {
        this.isOn = false;
        return `The ${this.name} is Off`;
    }
};
```

以及以下 server 对象：

```js
const server = {
    name: 'Dell PowerEdge T30',
    isOn: false
};
```

server 对象没有turnOn()和turnOff()方法。

要在 server 对象上执行 computer 对象的turnOn()方法，可以使用apply()方法，如下所示：

```js
let result = computer.turnOn.apply(server);
console.log(result); // The Dell PowerEdge T30 is On

let result = computer.turnOff.apply(server);
console.log(result); // The Dell PowerEdge T30 is Off
```