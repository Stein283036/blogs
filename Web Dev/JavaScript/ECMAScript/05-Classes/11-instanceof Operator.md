# JavaScript instanceof

## Introduction to the JavaScript instanceof operator

如果构造函数的原型 (constructor.prototype) 出现在对象的原型链中，instanceof 运算符将返回 true。

下面显示了instanceof运算符的语法：

```js
object instanceof contructor
```

在这个语法中：

- object 是要测试的对象。
- 构造函数是一个要测试的函数。

## JavaScript instanceof operator example

以下示例定义了 Person 类型并使用 instanceof 运算符来检查对象是否是该类型的实例：

```js
function Person(name) {
  this.name = name;
}

let p1 = new Person('John');

console.log(p1 instanceof Person); // true
```

它返回 true，因为 Person.prototype 出现在 p1 对象的原型链上。 p1的原型链是p1、Person.prototype和Object.prototype之间的链接：

<img src="https://www.javascripttutorial.net/wp-content/uploads/2022/01/JavaScript-instanceof.svg" alt="img" style="zoom: 80%;" />

以下也返回 true，因为 Object.prototype 出现在 p1 对象的原型链上：

```js
console.log(p1 instanceof Object); // true
```

## ES6 class and instanceof operator

以下示例定义了 Person 类并使用 instanceof 运算符来检查对象是否是该类的实例：

```js
class Person {
  constructor(name) {
    this.name = name;
  }
}

let p1 = new Person('John');

console.log(p1 instanceof Person); // true
```

## The instanceof operator and inheritance

以下示例定义了扩展 Person 类的 Employee 类：

```jsclass Person {
class Person {
  constructor(name) {
    this.name = name;
  }
}

class Employee extends Person {
  constructor(name, title) {
    super(name);
    this.title = title;
  }
}

let e1 = new Employee();

console.log(e1 instanceof Employee); // true
console.log(e1 instanceof Person); // true
console.log(e1 instanceof Object); // true
```

由于 e1 是 Employee 类的实例，因此它也是 Person 和 Object 类（基类）的实例。

## Symbol.hasInstance

在 ES6 中，instanceof 运算符使用 Symbol.hasInstance 函数来检查关系。Symbol.hasInstance() 接受一个对象，如果类型将该对象作为实例，则返回 true。例如：

```js
class Person {
  constructor(name) {
    this.name = name;
  }
}

let p1 = new Person('John');
typeof Symbol.hasInstance // symbol
console.log(Person[Symbol.hasInstance](p1)); // true
```

由于 Symbol.hasInstance 是在 Function 原型上定义的，因此默认情况下它在所有函数和类中自动可用。

可以将子类上的 Symbol.hasInstance 重新定义为静态方法。例如：

```js
class Person {
  constructor(name) {
    this.name = name;
  }
}

class Android extends Person {
  static [Symbol.hasInstance]() {
    return false;
  }
}

let a1 = new Android('Sonny');

console.log(a1 instanceof Android); // false
console.log(a1 instanceof Person); // false
```