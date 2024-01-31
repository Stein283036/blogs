# JavaScript Object Methods

## Introduction to the JavaScript object methods

对象是键/值对或属性的集合。当值是函数时，属性就变成方法。通常，使用方法来描述对象的行为。

例如，以下代码将greet方法添加到person对象中：

```js
let person = {
    firstName: 'John',
    lastName: 'Doe'
};

person.greet = function () {
    console.log('Hello!');
}

person.greet(); // Hello!
```

除了使用函数表达式之外，您还可以定义一个函数并将其分配给一个对象，如下所示：

```js
let person = {
    firstName: 'John',
    lastName: 'Doe'
};

function greet() {
    console.log('Hello, World!');
}

person.greet = greet;

person.greet();
```

## Object method shorthand

JavaScript 允许使用对象字面量语法定义对象的方法，如以下示例所示：

```js
let person = {
    firstName: 'John',
    lastName: 'Doe',
    greet: function () {
        console.log('Hello, World!');
    }
};
```

ES6 提供了简洁的方法语法，允许为对象定义方法：

```js
let person = {
    firstName: 'John',
    lastName: 'Doe',
    greet() {
        console.log('Hello, World!');
    }
};

person.greet();
```

### The this value

通常，方法需要访问对象的其他属性。

在方法内部，this 值引用调用该方法的对象。因此，可以使用 this 值访问属性，如下所示：

```js
this.propertyName
```

```js
let person = {
    firstName: 'John',
    lastName: 'Doe',
    greet: function () {
        console.log('Hello, World!');
    },
    getFullName: function () {
        return this.firstName + ' ' + this.lastName;
    }
};
console.log(person.getFullName()); // 'John Doe'
```



















