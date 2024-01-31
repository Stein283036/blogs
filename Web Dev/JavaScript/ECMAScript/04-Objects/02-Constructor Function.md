# JavaScript Constructor Function

## Introduction to JavaScript constructor functions

可以使用构造函数来定义自定义类型，并使用 new 运算符从该类型创建多个对象。

从技术上讲，构造函数是具有以下约定的常规函数：

- 构造函数的名称以大写字母开头，如 Person、Document 等。
- 构造函数只能使用 new 运算符调用。

请注意，ES6 引入了 class 关键字，允许定义自定义类型。**类只是构造函数的语法糖，具有一些增强功能。**

以下示例定义了一个名为 Person 的构造函数：

```js
function Person(firstName, lastName) {
    this.firstName = firstName;
    this.lastName = lastName;
}
```

要创建 Person 的新实例，请使用 new 运算符：

```js
let person = new Person('John','Doe');
```

基本上，new 运算符执行以下操作：

- 创建一个新的空对象并将其分配给 this 变量。
- 将参数“John”和“Doe”分配给对象的firstName 和lastName 属性。
- 返回 this 值。

它在功能上等同于以下内容：

```js
function Person(firstName, lastName) {
    // this = {};
    // add properties to this
    this.firstName = firstName;
    this.lastName = lastName;
    // return this;
}
```

## Adding methods to JavaScript constructor functions

对象可能具有操作其数据的方法。要向通过构造函数创建的对象添加方法，可以使用 this 关键字。例如：

```js
function Person(firstName, lastName) {
    this.firstName = firstName;
    this.lastName = lastName;

    this.getFullName = function () {
        return this.firstName + " " + this.lastName;
    };
}
```

现在，可以创建一个新的 Person 对象并调用 getFullName() 方法：

```js
let person = new Person("John", "Doe");
console.log(person.getFullName()); // John Doe
```

构造函数的问题在于，当创建 Person 的多个实例时， this.getFullName() 会在每个实例中重复，这样内存效率不高。

要解决此问题，可以使用原型，以便自定义类型的所有实例都可以共享相同的方法。

## Returning from constructor functions

通常，构造函数隐式返回设置为新创建对象的 this 。但如果它有 return 语句，则规则如下：

- 如果使用对象调用 return，构造函数将返回该对象而不是 this。
- 如果使用对象以外的值调用 return，则该值将被忽略。

## Calling a constructor function without the `new` keyword

从技术上讲，可以像常规函数一样调用构造函数，而无需使用 new 关键字，如下所示：

```js
let person = Person('John','Doe');
```

在这种情况下，Person 只是像常规函数一样执行。因此，Person 函数中的 this 并不绑定到 person 变量，而是绑定到全局对象。

如果尝试访问firstName或lastName属性，将收到错误：

```js
console.log(person.firstName);
TypeError: Cannot read property 'firstName' of undefined
```

同样，无法访问 getFullName() 方法，因为它绑定到全局对象。

为了防止在没有 new 关键字的情况下调用构造函数，ES6 引入了 new.target 属性。

如果使用 new 关键字调用构造函数，则 new.target 返回该函数的引用。否则，它返回 undefined。

下面向 Person 函数添加一条语句，以将 new.target 显示到控制台：

```js
function Person(firstName, lastName) {
    console.log(new.target);

    this.firstName = firstName;
    this.lastName  = lastName;

    this.getFullName = function () {
        return this.firstName + " " + this.lastName;
    };
}
```

以下返回未定义，因为 Person 构造函数的调用方式与常规函数类似：

```js
let person = Person("John", "Doe"); // undefined
```

但是，以下代码返回对 Person 函数的引用，因为它被称为 new 关键字：

```js
let person = new Person("John", "Doe"); // [Function: Person]
```

通过使用 new.target，您可以强制构造函数的调用者使用 new 关键字。否则，可能会抛出如下错误：

```js
function Person(firstName, lastName) {
    if (!new.target) {
        throw Error("Cannot be called without the new keyword");
    }

    this.firstName = firstName;
    this.lastName = lastName;
}
```

或者，如果构造函数的用户不使用 new 关键字，则可以通过创建新的 Person 对象来使语法更加灵活：

```js
function Person(firstName, lastName) {
    if (!new.target) {
        return new Person(firstName, lastName);
    }

    this.firstName = firstName;
    this.lastName = lastName;
}

let person = Person("John", "Doe");

console.log(person.firstName);
```

这种模式经常用于 JavaScript 库和框架中，以使语法更加灵活。































