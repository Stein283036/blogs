# JavaScript Computed Property

## Introduction to JavaScript Computed Property

ES6 允许在方括号 [] 中使用表达式。然后它将使用表达式的结果作为对象的属性名称。例如：

```js
let propName = 'c';

const rank = {
  a: 1,
  b: 2,
  [propName]: 3,
};

console.log(rank.c); // 3
```

在此示例中，[propName] 是 rank 对象的计算属性。属性名称源自 propName 变量的值。

当访问rank对象的c属性时，JavaScript会计算propName并返回该属性的值。

与对象字面量一样，可以将计算属性用于类的 getter 和 setter。例如：

```js
let name = 'fullName';

class Person {
  constructor(firstName, lastName) {
    this.firstName = firstName;
    this.lastName = lastName;
  }
  get [name]() {
    return `${this.firstName} ${this.lastName}`;
  }
}

let person = new Person('John', 'Doe');
console.log(person.fullName); // John Doe
```