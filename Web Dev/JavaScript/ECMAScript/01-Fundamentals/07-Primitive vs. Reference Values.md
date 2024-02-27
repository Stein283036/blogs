# Primitive vs. Reference Values

JavaScript has two different types of values:

- Primitive values
- Reference values

Primitive values are atomic pieces of data while reference values are objects that might consist of multiple values.

## Stack and heap memory

当声明变量时，JavaScript 引擎会在两个内存位置为它们分配内存：堆栈和堆。

静态数据是在编译时大小固定的数据。静态数据包括：

- Primitive values (null, undefined, boolean, number, string, symbol, and BigInt)
- Reference values that refer to objects.

由于静态数据的大小不会改变，因此 JavaScript 引擎会为静态数据分配固定大小的内存空间并将其存储在堆栈中。

与堆栈不同，JavaScript 在堆上存储对象（和函数）。JavaScript 引擎不会为这些对象分配固定数量的内存。相反，它会根据需要分配更多空间。

## Dynamic Properties

引用允许随时添加、更改或删除属性。例如：

```javascript
let person = {
  name: 'John',
  age: 25,
};

// add the ssn property
person.ssn = '123-45-6789';
// change the name
person.name = 'John Doe';
// delete the age property
delete person.age;
console.log(person); // { name: 'John Doe', ssn: '123-45-6789' }
```

与引用值不同，原始值不能具有属性。这意味着无法将属性添加到原始值。

JavaScript 允许向原始值添加属性。但是，它不会产生任何效果。例如：

```js
let name = 'John';
name.alias = 'Knight';
console.log(name.alias); // undefined
```

## Copying values

当将一个变量的原始值分配给另一个变量时，JavaScript 引擎会创建该值的副本并将其分配给该变量。

```js
let age = 25;
let newAge = age;
```

在幕后，JavaScript 引擎创建原始值 25 的副本并将其分配给 newAge 变量。

在堆栈内存中，newAge 和age 是单独的变量。如果更改一个变量的值，不会影响另一个变量。

当您将一个变量的引用值分配给另一个变量时，JavaScript 引擎会创建一个引用，以便两个变量都引用堆内存上的同一对象。这意味着如果更改一个变量，它将影响另一个变量。

```js
let person = {
  name: 'John',
  age: 25,
};

let member = person;

member.age = 26;

console.log(person);
console.log(member);
```

![img](https://www.javascripttutorial.net/wp-content/uploads/2022/01/JavaScript-copy-a-reference-value.svg)
