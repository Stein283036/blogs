# A Basic Guide to Enumerable Properties of an Object in JavaScript

## Introduction to JavaScript enumerable properties

使用 for...in 循环或 Objects.keys() 方法迭代可枚举属性，Object.keys() 方法只能迭代对象自己的属性。

In JavaScript, an object is an unordered list of key-value pairs. **The key is usually a string or a symbol.** The value can be a value of any primitive type (string, boolean, number, undefined, or null), an object, or a function.

以下示例使用对象字面量语法创建一个新对象：

```js
const person = {
    firstName: 'John',
    lastName: 'Doe
};
```

person 对象有两个属性：firstName 和lastName。

An object property has several internal **attributes** including value, writable, enumerable and configurable. See the Object properties for more details.

enumerable 属性决定当使用 for...in 循环或 Object.keys() 方法枚举对象的属性时，属性是否可访问。

默认情况下，通过简单赋值或属性初始值设定项创建的所有属性都是可枚举的。例如：

```js
const person = {
    firstName: 'John',
    lastName: 'Doe'
};
person.age = 25;
for (const key in person) {
    console.log(key);
}
firstName
lastName
age
```

To change the internal `enumerable` **attribute** of a property, you use the `Object.defineProperty()` method. For example:

```js
const person = {
    firstName: 'John',
    lastName: 'Doe'
};
person.age = 25;
Object.defineProperty(person, 'ssn', {
    enumerable: false,
    value: '123-456-7890'
});
for (const key in person) {
    console.log(key);
}
firstName
lastName
age
```

In this example, the `ssn` property is created with the `enumerable` flag sets to `false`, therefore it does not show up in the `for...in` loop.

ES6 provides a method `propertyIsEnumerable()` that determines whether or not a property is enumerable. It returns `true` if the property is enumerable; otherwise `false`. For example:

```js
const person = {
    firstName: 'John',
    lastName: 'Doe'
};
person.age = 25;
Object.defineProperty(person, 'ssn', {
    enumerable: false,
    value: '123-456-7890'
});
console.log(person.propertyIsEnumerable('firstName')); // => true
console.log(person.propertyIsEnumerable('lastName')); // => true
console.log(person.propertyIsEnumerable('age')); // => true
console.log(person.propertyIsEnumerable('ssn')); // => false
```