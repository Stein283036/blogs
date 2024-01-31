# JavaScript Prototypal Inheritance

## Introduction to JavaScript prototypal inheritance

如果使用过其他面向对象的编程语言（例如 Java 或 C++），就会熟悉继承概念。

在这种编程范式中，类是创建对象的蓝图。如果希望新类重用现有类的功能，可以创建一个扩展现有类的新类。这称为经典继承。

JavaScript 不使用经典继承。相反，它使用原型继承。

在原型继承中，一个对象通过原型链接从另一个对象“继承”属性。

## JavaScript prototypal inheritance and `__proto__`

下面定义了一个 person 对象：

```js
let person = {
    name: "John Doe",
    greet: function () {
        return "Hi, I'm " + this.name;
    }
};
```

在此示例中，person 对象有一个属性和一个方法：

- name 是存储人名的属性。

- greet 是一个以字符串形式返回问候语的方法。

默认情况下，JavaScript 引擎提供内置的 Object() 函数和可由 Object.prototype 引用的匿名对象：

![JavaScript Prototype](https://www.javascripttutorial.net/wp-content/uploads/2022/01/JS-prototype.svg)

这意味着 person 对象可以调用 Object.prototype 引用的匿名对象中定义的任何方法。

```js
console.log(person.toString());
[object Object]
```

[object Object] 是对象的默认字符串表示形式。

当通过 person 调用 toString() 方法时，JavaScript 引擎无法在 person 对象上找到它。因此，它沿着原型链寻找Object.prototype对象中的方法。

要访问 person 对象的原型，可以使用 `__proto__ ` 属性，如下所示

```js
console.log(person.__proto__);
```

>  请注意，永远不应该在生产代码中使用 __proto__ 属性。请仅将其用于演示目的。

下面显示了 `person.__proto__` 和 Object.prototype 引用了同一个对象：

下面定义了具有teach()方法的teacher对象：

```js
let teacher = {
    teach: function (subject) {
        return "I can teach " + subject;
    }
};
```

与 person 对象一样，`teacher.__proto__` 引用了 Object.prototype，如下图所示：

![img](https://www.javascripttutorial.net/wp-content/uploads/2022/01/JavaScript-prototypal-inheritance-inherits-from-Object.svg)



如果想让teacher对象访问person对象的所有方法和属性，可以将teacher对象的原型设置为person对象，如下所示：

```js
teacher.__proto__ = person;
```

![img](https://www.javascripttutorial.net/wp-content/uploads/2022/01/JavaScript-prototypal-inheritance-example.svg)



现在，teacher 对象可以通过原型链从 person 对象访问 name 属性和greet() 方法：

```js
console.log(teacher.name);
console.log(teacher.greet());
John Doe
Hi, I'm John Doe
```

当您在教师对象上调用greet()方法时，JavaScript引擎首先在teacher对象中找到它。

由于JavaScript引擎无法在teacher对象中找到该方法，因此它沿着原型链在person对象中搜索该方法。因为JavaScript引擎可以在person对象中找到greet()方法，所以它会执行该方法。

在JavaScript中，我们说teacher对象继承了person对象的方法和属性。这种继承称为原型继承（**prototypal inheritance**）。

## A standard way to implement prototypal inheritance in ES5

ES5 通过使用 Object.create() 方法提供了一种处理原型继承的标准方法。

> 请注意，现在应该使用较新的 ES6 类和 extends 关键字来实现继承。简单多了。

Object.create() 方法创建一个新对象并使用现有对象作为新对象的原型：

```js
Object.create(proto, [propertiesObject])
```

Object.create() 方法接受两个参数：

- 第一个参数 (proto) 是用作新对象的原型对象。
- 第二个参数 (propertiesObject)（如果提供）是一个可选对象，用于为新对象定义其他属性。

假设有一个 person 对象：

```js
let person = {
    name: "John Doe",
    greet: function () {
        return "Hi, I'm " + this.name;
    }
};
```

以下代码使用 person 对象的 `__proto__` 创建一个空的 teacher 对象：

```js
let teacher = Object.create(person);
```

之后，可以为教师对象定义属性：

```js
teacher.name = 'Jane Doe';
teacher.teach = function (subject) {
        return "I can teach " + subject;
}
```

或者可以在一条语句中执行所有这些步骤，如下所示：

```js
let teacher = Object.create(person, {
    name: { value: 'John Doe' } ,
    teach: { value: function(subject) {
        return "I can teach " + subject;
    }}
});
```

ES5还引入了Object.getPrototypeOf()方法，该方法返回对象的原型。例如：

``` js
console.log(Object.getPrototypeOf(teacher) === person); // true
```





























