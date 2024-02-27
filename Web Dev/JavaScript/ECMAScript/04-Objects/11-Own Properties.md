# Understanding Own Properties of an Object in JavaScript

在 JavaScript 中，对象是属性的集合，其中每个属性都是一个键值对。

```js
const person = {
    firstName: 'John',
    lastName: 'Doe'
};
```

person 对象有两个属性：firstName 和 lastName。

JavaScript 使用原型继承。因此，对象的属性可以是自己的，也可以是继承的。

直接在对象上定义的属性是自己的，而对象从其原型接收的属性是继承的。

下面创建一个名为 employee 的对象，该对象继承自 person 对象：

```js
const employee = Object.create(person, {
    job: {
        value: 'JS Developer',
        enumerable: true
    }
});
```

employee 对象有自己的属性 job，并从其原型 person 继承了 firstName 和 lastName 属性。

如果属性是自己的，则 hasOwnProperty() 方法返回 true。

```js
console.log(employee.hasOwnProperty('job')); // => true
console.log(employee.hasOwnProperty('firstName')); // => false
console.log(employee.hasOwnProperty('lastName')); // => false
```
