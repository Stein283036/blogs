# JavaScript Class Expressions

## Introduction to JavaScript class expressions

与函数类似，类也有表达形式。类表达式提供了另一种定义新类的方法。

类表达式不需要在 class 关键字后添加标识符。可以在变量声明中使用类表达式并将其作为参数传递到函数中。

```js
let Person = class {
    constructor(name) {
        this.name = name;
    }
    getName() {
        return this.name;
    }
}
```

以下创建 Person 类表达式的实例。它的语法与类声明相同。

```js
let person = new Person('John Doe');
```

与类声明一样，类表达式的类型也是一个函数：

```js
console.log(typeof Person); // function
```

与函数表达式类似，类表达式不会被提升。这意味着在定义类表达式之前不能创建类的实例。

## First-class citizen

JavaScript 类是一等公民。这意味着可以将类传递给函数，从函数返回它，并将其分配给变量。

在编程语言中，一等公民是指具有以下特性的实体：

1. 可以被赋值给变量。
2. 可以作为参数传递给函数。
3. 可以作为函数的返回值。
4. 可以存储在数据结构中。

```js
function factory(aClass) {
    return new aClass();
}

let greeting = factory(class {
    sayHi() { console.log('Hi'); }
});

greeting.sayHi(); // 'Hi'
```

首先，定义一个factory()函数，它将类表达式作为参数并返回类的实例：

```js
function factory(aClass) {
    return new aClass();
}
```

其次，将未命名的类表达式传递给factory()函数并将其结果分配给greeting变量：

```js
let greeting = factory(class {
    sayHi() { console.log('Hi'); }
});
```

类表达式有一个名为 sayHi() 的方法。greeting 变量是类表达式的一个实例。

第三，调用greeting对象的sayHi()方法：

```js
greeting.sayHi(); // 'Hi'
```

## Singleton

Singleton 是一种将类的实例化限制为单个实例的设计模式。它确保在整个系统中只能创建一个类的一个实例。

类表达式可用于通过立即调用类构造函数来创建单例。

为此，可以将 new 运算符与类表达式结合使用，并在类声明末尾包含括号，如下例所示：

```js
let app = new class {
    constructor(name) {
        this.name = name;
    }
    start() {
        console.log(`Starting the ${this.name}...`);
    }
}('Awesome App');

app.start(); // Starting the Awesome App...
```

类表达式的计算结果是一个类。因此，可以通过在表达式后面放置括号来立即调用其构造函数：

此表达式返回分配给 app 变量的类表达式的实例。
