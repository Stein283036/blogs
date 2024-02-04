# JavaScript Object Destructuring

## Introduction to the JavaScript object destructuring assignment

假设有一个具有两个属性的 person 对象：firstName 和 lastName。

```js
let person = {
    firstName: 'John',
    lastName: 'Doe'
};
```

在 ES6 之前，当想将 person 对象的属性分配给变量时，通常会这样做：

```js
let firstName = person.firstName;
let lastName = person.lastName;
```

ES6 引入了对象解构语法，它提供了另一种将对象属性分配给变量的方法：

```js
let { firstName: fname, lastName: lname } = person;
```

在此示例中，firstName 和 lastName 属性分别分配给 fName 和 lName 变量。冒号（:）之前的标识符是对象的属性，冒号之后的标识符是变量。

如果变量与对象的属性具有相同的名称，则可以使代码更加简洁，如下所示：

```js
let { firstName, lastName } = person;
console.log(firstName); // 'John'
console.log(lastName); // 'Doe'
```

当使用对象解构将不存在的属性分配给变量时，该变量将设置为未定义。例如：

```js
let { firstName, lastName, middleName } = person;
console.log(middleName); // undefined
```

## Setting default values

当对象的属性不存在时，可以为变量分配默认值。例如：

```js
let person = {
    firstName: 'John',
    lastName: 'Doe',
    currentAge: 28
};

let { firstName, lastName, middleName = '', currentAge: age = 18 } = person;

console.log(middleName); // ''
console.log(age); // 28
```

## Destructuring a null object

在某些情况下，函数可能返回对象或 null。例如：

```js
function getPerson() {
    return null;
}
```

并且使用对象解构赋值：

```js
let { firstName, lastName } = getPerson();

console.log(firstName, lastName);
TypeError: Cannot destructure property 'firstName' of 'getPerson(...)' as it is null.
```

为了避免这种情况，可以使用 OR 运算符 (||) 将 null 对象回退为空对象：

现在，不会发生任何错误。并且firstName和lastName的值是 undefined。

## Nested object destructuring

Assuming that you have an `employee` object which has a `name` object as the property:

```js
let employee = {
    id: 1001,
    name: {
        firstName: 'John',
        lastName: 'Doe'
    }
};
```

The following statement destructures the properties of the nested `name` object into individual variables:

```js
let {
    name: {
        firstName: f,
        lastName: l
    }
} = employee;

console.log(f); // John
console.log(l); // Doe
```

## Destructuring function arguments

Suppose you have a function that displays the person object:

```js
let display = (person) => console.log(`${person.firstName} ${person.lastName}`);

let person = {
    firstName: 'John',
    lastName: 'Doe'
};

display(person);
```

可以像这样解构传递给函数的对象参数：

```js
let display = ({firstName, lastName}) => console.log(`${firstName} ${lastName}`);
let person = {
    firstName: 'John',
    lastName: 'Doe'
};
display(person);
```

它看起来不那么冗长，尤其是当使用参数对象的许多属性时。这种技术在 React 中经常使用。