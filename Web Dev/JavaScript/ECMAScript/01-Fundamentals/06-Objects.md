# Objects

## Introduction to the JavaScript objects

在 JavaScript 中，对象是键值对的无序集合。每个键值对称为属性。

JavaScript 为您提供了多种创建对象的方法。最常用的一种是使用对象字面量表示法。

```js
let empty = {};
```

要创建具有属性的对象，请在大括号内使用键：值。

```js
let person = {
    firstName: 'John',
    lastName: 'Doe'
};
```

## Accessing properties

要访问对象的属性，可以使用两种表示法之一：dot notation和array-like notation。

当属性名称包含空格时，需要将其放在引号内。

例如，以下address对象具有“建筑物编号”作为属性：

```js
let address = {
    'building no': 3960,
    street: 'North 1st street',
    state: 'CA',
    country: 'USA'
};
```

要访问“building no”属性，您需要使用类似数组的表示法：

```js
address['building no'];
```

> 请注意，在对象的属性名称中使用空格不是一个好习惯。

读取不存在的属性将导致`undefined`。例如：

```js
console.log(address.district);
undefined
```

## Modifying the value of a property

要更改属性的值，可以使用赋值运算符 (=)。

```js
let person = {
    firstName: 'John',
    lastName: 'Doe'
};

person.firstName = 'Jane';

console.log(person);
{ firstName: 'Jane', lastName: 'Doe' }
```

## Adding a new property to an object

与 Java 和 C# 等其他编程语言中的对象不同，您可以在创建对象后向对象添加属性。

```js
person.age = 25;
```

## Deleting a property of an object

要删除对象的属性，可以使用删除运算符：

```js
delete objectName.propertyName;
```

## Checking if a property exists

要检查对象中是否存在属性，请使用 in 运算符：

```js
propertyName in objectName
```



























