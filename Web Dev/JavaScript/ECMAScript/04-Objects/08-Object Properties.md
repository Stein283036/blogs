# JavaScript Object Properties

## Object Property types

JavaScript specifies the characteristics of properties of objects via internal **attributes** surrounded by the two pairs of square brackets, e.g., `[[Enumerable]]`.

对象有两种类型的属性：数据属性（data properties）和访问器属性（accessor properties）。

### Data properties

A data property contains a single location for a data value. A data property has four attributes(PropertyDescriptor):

- [[Configurarable]] – determines whether a property can be redefined or removed via delete operator.

  **可配置性（Configurable）**：指示属性是否可删除和是否可修改属性的特性。如果为 `true`，则属性可以被删除，属性的特性（包括 `writable`、`enumerable` 和 `configurable`）可以修改；如果为 `false`，则属性不可被删除，属性的特性不可被修改。

- [[Enumerable]] – indicates if a property can be returned in the for...in loop.

- [[Writable]] – specifies that the value of a property can be changed.

- [[Value]] – contains the actual value of a property.

默认情况下，直接在对象上定义的所有属性的 [[Configurable]] 、 [[Enumerable]] 和 [[Writable]] 属性设置为 true。 [[Value]] 属性的默认值为 undefined。

例如，以下创建一个具有两个属性 firstName 和 lastName 的 person 对象，并将 configurable、enumerable 和 writable attributes 设置为 true，并将它们的值分别设置为 “John” 和 “Doe”：

```js
let person = {
    firstName: 'John',
    lastName: 'Doe'
};
```

To change any attribute of a property, use the `Object.defineProperty()` method.

Object.defineProperty() 方法接受三个参数：

- An object.
- A property name of the object.
- A property descriptor object that has four properties: `configurable`, `enumerable`, `writable`, and `value`.

如果使用 Object.defineProperty() 方法定义对象的属性，除非另有指定，否则 [[Configurable]]、[[Enumerable]] 和 [[Writable]] 的默认值将设置为 false。

以下示例创建一个具有 Age 属性的 person 对象：

```js
let person = {};
person.age = 25;
```

由于 [[Configurable]] 属性的默认值设置为 true，因此可以通过删除运算符将其删除：

```js
delete person.age
console.log(person.age); // undefined
```

以下示例创建一个 person 对象并使用 Object.defineProperty() 方法向其添加 ssn 属性：

```js
'use strict';
let person = {};
Object.defineProperty(person, 'ssn', {
    configurable: false,
    value: '012-38-9119'
});
delete person.ssn;
TypeError: Cannot delete property 'ssn' of #<Object>
```

在此示例中，configurable 属性设置为 false。因此，删除 ssn 属性会导致错误。

此外，一旦将属性定义为 non-configurable，就无法将其更改为 configurable。

默认情况下，对象上定义的所有属性的 enumerable 属性都是 true。这意味着可以使用 for...in 循环迭代所有对象属性：

```js
let person = {};
person.age = 25;
person.ssn = '012-38-9119';
for (let property in person) {
    console.log(property);
}
age
ssn
```

以下通过将 enumerable 属性设置为 false 使 ssn 属性不可枚举。

```js
let person = {};
person.age = 25;
person.ssn = '012-38-9119';
Object.defineProperty(person, 'ssn', {
    enumerable: false
});
for (let prop in person) {
    console.log(prop);
}
age
```

### Accessor properties

访问器属性是使用 getter 和 setter 函数定义的属性，它们并不存储数据值，而是在读取或设置属性时调用相关的函数。

Similar to data properties, accessor properties also have `[[Configurable]]` and `[[Enumerable]]` attributes.

**但访问器属性具有 [[Get]] 和 [[Set]]，而不是 [[Value]] 和 [[Writable]]。**

当从访问器属性读取数据时，会自动调用 [[Get]] 函数以返回值。 [[Get]] 函数的默认返回值是 undefined。

如果将值分配给访问器属性，则会自动调用 [[Set]] 函数。

要定义访问器属性，**必须**使用 Object.defineProperty() 方法。

```js
let person = {
    firstName: 'John',
    lastName: 'Doe'
}
Object.defineProperty(person, 'fullName', {
    get: function () {
        return this.firstName + ' ' + this.lastName;
    },
    set: function (value) {
        let parts = value.split(' ');
        if (parts.length == 2) {
            this.firstName = parts[0];
            this.lastName = parts[1];
        } else {
            throw 'Invalid name format';
        }
    }
});
console.log(person.fullName); // 'John Doe'
```

在这个例子中：

- 首先，定义包含两个属性的 person 对象：firstName 和 lastName。
- 然后，将 fullName 属性作为访问器属性添加到 person 对象。

在 fullname 访问器属性中：

- [[Get]] 返回由 firstName、空格和 lastName 连接而成的全名。
- [[Set]] 方法按空格分割参数，并分配名称相应部分的 firstName 和 lastName 属性。
- 如果 fullName 的格式不正确，即名字、空格和姓氏，则会抛出错误。

## Define multiple properties: Object.defineProperties()

在 ES5 中，可以使用 Object.defineProperties() 方法在单个语句中定义多个属性。

```js
let product = {};
Object.defineProperties(product, {
    name: {
        value: 'Smartphone'
    },
    price: {
        value: 799
    },
    tax: {
        value: 0.1
    },
    netPrice: {
        get: function () {
            return this.price * (1 + this.tax);
        }
    }
});
console.log('The net price of a ' + product.name + ' is ' + product.netPrice.toFixed(2) + ' USD');
// The net price of a Smartphone is 878.90 USD
```

在此示例中，我们为 product 对象定义了三个数据属性：name、price 和 tax 以及一个访问器属性 netPrice。

## JavaScript object property descriptor

Object.getOwnPropertyDescriptor() 方法允许获取属性的描述符对象。 Object.getOwnPropertyDescriptor() 方法采用两个参数：

1. An object
2. A property of the object

It returns a descriptor object that describes a property. The descriptor object has four properties: configurable, enumerable, writable, and value.

以下示例获取上一示例中 product 对象的 name 和 netPrice 属性的描述符对象。

```js
Object.getOwnPropertyDescriptor(product, "name");
configurable: false
enumerable: false
value: "Smartphone"
writable: false

Object.getOwnPropertyDescriptor(product, "netPrice");
configurable: false
enumerable: false
get: ƒ ()
set: undefined
```
