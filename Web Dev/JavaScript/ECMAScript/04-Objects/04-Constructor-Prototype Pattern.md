# JavaScript Constructor/Prototype Pattern

## Introduction to the JavaScript Constructor / Prototype pattern

构造函数和原型模式的组合是 ES5 中定义自定义类型的最常见方法。在这个模式中：

- 构造函数模式定义对象属性。
- 原型模式定义了对象方法。

通过使用此模式，自定义类型的所有对象都共享原型中定义的方法。此外，每个对象都有自己的属性。

这种构造函数/原型模式吸收了构造函数和原型模式的最佳部分。

## JavaScript Constructor / Prototype example

假设要定义一个名为 Person 的自定义类型，它具有：

- 两个属性 firstName 和 lastName。
- 一个方法 getFullName()。

首先，使用构造函数初始化属性：

```js
function Person(firstName, lastName) {
    if (!new.target) {
        return new Person(firstName, lastName);
    }
    this.firstName = firstName;
    this.lastName = lastName;
}
```

在幕后，JavaScript 引擎定义了一个用圆圈表示的 Person 函数和一个用正方形表示的匿名对象。

Person 函数具有引用匿名对象的原型属性。匿名对象有一个引用 Person 函数的构造函数属性：

![JS prototype- Person prototype](https://www.javascripttutorial.net/wp-content/uploads/2022/01/JS-prototype-Person-prototype.svg)

其次，在 Person 函数的原型对象中定义 getFullName() 方法：

```js
Person.prototype.getFullName = function() {
    return this.firstName + ' ' + this.lastName;
}
```

JavaScript 在 Person.prototype 对象上定义了 getFullName() 方法，如下所示：

![img](https://www.javascripttutorial.net/wp-content/uploads/2022/01/JS-prototype-constructor-pattern.svg)

第三，创建 Person 类型的多个实例：

```js
let p1 = new Person("John", "Doe");
let p2 = new Person("Jane", "Doe");

console.log(p1.getFullName());
console.log(p2.getFullName());
// 输出
'John Doe'
'Jane Doe'
```

Javascript 创建两个对象 p1 和 p2。这些对象通过 [[Prototype]] 链接到 Person.prototype 对象：

![img](https://www.javascripttutorial.net/wp-content/uploads/2022/01/JavaScript-constructor-prototype-pattern-example.svg)

每个对象都有自己的属性 firstName 和 lastName。但是，它们共享相同的 getFullName() 方法。

当对 p1 或 p2 对象调用 getFullName() 方法时，JavaScript 引擎会搜索这些对象的方法。因为 JavaScript 引擎在那里找不到该方法，所以它遵循原型链接并在 Person.prototype 对象中搜索该方法。

## Classes in ES6

ES6 引入了 class 关键字，使构造函数/原型模式更易于使用。例如，以下使用 class 关键字定义相同的 Person 类型：

```js
class Person {
	constructor(firstName, lastName) {
		this.firstName = firstName;
		this.lastName = lastName;
	}
	getFullName() {
		return this.firstName + " " + this.lastName;
	}
}

let p1 = new Person('John', 'Doe');
let p2 = new Person('Jane', 'Doe');

console.log(p1.getFullName());
console.log(p2.getFullName());
```

在此语法中，类将属性初始化移至构造函数方法。它还将 getFullName() 方法定义在与构造函数相同的位置。

类语法看起来更干净、更简洁。然而，它是构造函数/原型模式的语法糖，并具有一些增强功能。
