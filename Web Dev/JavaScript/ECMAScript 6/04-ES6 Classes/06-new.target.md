# Introduction to JavaScript new.target Metaproperty

## Introduction to JavaScript new.target

ES6 提供了一个名为 new.target 的元属性，允许检测是否使用 new 运算符调用了函数或构造函数。

new.target 由 new 关键字、一个点和 target 属性组成。 new.target 在所有函数中都可用。

然而，在箭头函数中，new.target 是属于周围函数的。

new.target 对于在运行时检查函数是作为函数还是作为构造函数执行非常有用。还可以方便地确定在父类中使用 new 运算符调用的特定派生类。

## JavaScript new.target in functions

让我们看看下面的 Person 构造函数：

```js
function Person(name) {
    this.name = name;
}
```

可以使用 new 运算符从 Person 函数创建一个新对象，如下所示：

```js
let john = new Person('John');
console.log(john.name); // john
```

或者可以将 Person 作为函数调用：

```js
Person('Lily');
```

由于 this 设置为全局对象，即在 Web 浏览器中运行 JavaScript 时的 window 对象，因此 name 属性将添加到 window 对象，如下所示：

```js
console.log(window.name); //Lily
```

为了帮助检测是否使用 new 运算符调用函数，可以使用 new.target 元属性。

在常规函数调用中，new.target 返回 undefined。如果使用 new 运算符调用该函数，则 new.target 返回对该函数的引用。

假设不希望 Person 作为普通函数被调用，可以使用 new.target，如下所示：

```js
function Person(name) {
    if (!new.target) {
        throw "must use new operator with Person";
    }
    this.name = name;
}
```

现在，使用 Person 的唯一方法是使用 new 运算符实例化一个对象。如果尝试将其作为常规函数调用，则会出现错误。

## JavaScript new.target in constructors

在类构造函数中，new.target 指的是由 new 运算符直接调用的构造函数。

```js
class Person {
    constructor(name) {
        this.name = name;
        console.log(new.target.name);
    }
}

class Employee extends Person {
    constructor(name, title) {
        super(name);
        this.title = title;
    }
}

let john = new Person('John Doe'); // Person
let lily = new Employee('Lily Bush', 'Programmer'); // Employee
```

在此示例中，new.target.name 是 new.target 的构造函数引用的人类友好名称。