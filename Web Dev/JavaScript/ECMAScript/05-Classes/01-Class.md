# JavaScript Class

A JavaScript class is a blueprint for creating objects. A class encapsulates data and functions that manipulate data.

与 Java 和 C# 等其他编程语言不同，JavaScript **类是原型继承之上的语法糖**。

换句话说，ES6 的类只是特殊的函数。

## Classes before ES6 revisited

在 ES6 之前，JavaScript 没有类的概念。为了模仿类，经常使用构造函数/原型模式，如下例所示：

```js
function Person(name) {
    this.name = name;
}

Person.prototype.getName = function () {
    return this.name;
};

var john = new Person("John Doe");
console.log(john.getName()); // John Doe
```

## ES6 class declaration

ES6 引入了一种用于声明类的新语法，如下例所示：

```js
class Person {
    constructor(name) {
        this.name = name;
    }
    getName() {
        return this.name;
    }
}
```

在 Person 类中，可以在 constructor() 中初始化实例的属性。当实例化类的对象时，JavaScript 会自动调用 constructor() 方法。

下面创建一个新的Person对象，它会自动调用Person类的constructor()：

```js
let john = new Person("John Doe");
```

getName() 被称为 Person 类的方法。与构造函数一样，可以使用以下语法调用类的方法：

```js
let name = john.getName();
console.log(name); // "John Doe"
```

要验证类是特殊函数这一事实，可以使用 typeof 运算符来检查 Person 类的类型。

```js
console.log(typeof Person); // function
```

john 对象也是 Person 和 Object 类型的实例：

```js
console.log(john instanceof Person); // true
console.log(john instanceof Object); // true
```

## Class vs. Custom type

尽管类和通过构造函数定义的自定义类型之间有相似之处，但仍存在一些重要的区别。

首先，类声明不像函数声明那样被提升。

例如，如果将以下代码放置在 Person 类声明部分上方，将收到 ReferenceError。

```js
let john = new Person("John Doe");
Uncaught ReferenceError: Person is not defined

class Person {
    ...
}
```

其次，类中的所有代码都会自动以严格模式执行。而且你无法改变这种行为。

第三，类方法是不可枚举的。如果使用构造函数/原型模式，则必须使用 Object.defineProperty() 方法使属性不可枚举。

最后，在不使用 new 运算符的情况下调用类构造函数将导致错误，如以下示例所示。

```js
let john = Person("John Doe");
Uncaught TypeError: Class constructor Person cannot be invoked without 'new'
```























