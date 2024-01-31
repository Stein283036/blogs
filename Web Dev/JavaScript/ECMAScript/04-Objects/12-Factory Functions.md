# JavaScript Factory Functions

## Introduction to the factory functions in JavaScript

工厂函数是返回新对象的函数。下面创建一个名为 person1 的 person 对象：

```js
let person1 = {
  firstName: 'John',
  lastName: 'Doe',
  getFullName() {
    return this.firstName + ' ' + this.lastName;
  },
};
console.log(person1.getFullName()); // John Doe
```

person1 对象有两个属性：firstName 和 lastName，以及一个返回全名的方法 getFullName()。

假设需要创建另一个名为 person2 的类似对象，可以复制代码如下：

```js
let person2 = {
  firstName: 'Jane',
  lastName: 'Doe',
  getFullName() {
    return this.firstName + ' ' + this.lastName;
  },
};
console.log(person2.getFullName()); // Jane Doe
```

在此示例中，person1 和 person2 对象具有相同的属性和方法。

问题在于，要创建的对象越多，重复的代码就越多，占用的内存空间也越多。

为了避免再次复制相同的代码，可以定义一个创建 person 对象的函数：

```js
function createPerson(firstName, lastName) {
  return {
    firstName: firstName,
    lastName: lastName,
    getFullName() {
      return firstName + ' ' + lastName;
    },
  };
}
```

当一个函数创建并返回一个新对象时，它被称为工厂函数。 createPerson() 是一个工厂函数，因为它返回一个新的 person 对象。

```js
let person1 = createPerson('John', 'Doe');
let person2 = createPerson('Jane', 'Doe');
```

当创建一个对象时，JavaScript 引擎会为其分配内存。如果创建许多 person 对象，JavaScript 引擎需要大量内存空间来存储这些对象。

但是，每个 person 对象都有相同 getFullName() 方法的副本。这不是高效的内存管理。

为了避免在每个对象中重复相同的 getFullName() 函数，可以从 person 对象中删除 getFullName() 方法：

并将此方法移至另一个对象：

```js
var personActions = {
  getFullName() {
    return this.firstName + ' ' + this.lastName;
  },
};
```

并且在对 person 对象调用 getFullName() 方法之前，可以将 personActions 对象的方法分配给 person 对象，如下所示：

```js
let person1 = createPerson('John', 'Doe');
let person2 = createPerson('Jane', 'Doe');

person1.getFullName = personActions.getFullName;
person2.getFullName = personActions.getFullName;

console.log(person1.getFullName());
console.log(person2.getFullName());
```

如果对象有许多方法，则此方法不可扩展，因为必须手动单独分配它们。这就是 Object.create() 方法发挥作用的原因。

## The Object.create() method

Object.create() 方法使用现有对象作为新对象的原型创建一个新对象：

```js
Object.create(proto, [propertiesObject])
```

```js
var personActions = {
  getFullName() {
    return this.firstName + ' ' + this.lastName;
  },
};

function createPerson(firstName, lastName) {
  let person = Object.create(personActions);
  person.firstName = firstName;
  person.lastName = lastName;
  return person;
}
```

现在，可以创建 person 对象并调用 personActions 对象的方法：

```js
let person1 = createPerson('John', 'Doe');
let person2 = createPerson('Jane', 'Doe');

console.log(person1.getFullName());
console.log(person2.getFullName());
```

该代码工作得很好。然而，在实践中，很少会使用工厂函数。相反，可以使用类或构造函数/原型模式。