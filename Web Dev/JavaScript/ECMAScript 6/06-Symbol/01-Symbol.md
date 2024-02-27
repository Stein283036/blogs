# The Ultimate Guide to JavaScript Symbol

根据规范，只有两种原始类型可以用作对象属性键：

- 字符串类型
- symbol 类型

否则，如果使用另一种类型，例如数字，它会被自动转换为字符串。所以 `obj[1]` 与 `obj["1"]` 相同，而 `obj[true]` 与 `obj["true"]` 相同。

symbol 属性不参与 `for..in` 循环。

```javascript
let id = Symbol("id");
let user = {
  name: "John",
  age: 30,
  [id]: 123
};

for (let key in user) alert(key); // name, age（没有 symbol）

alert("Direct: " + user[id]); // Direct: 123
```

Object.keys(user) 也会忽略它们。这是一般“隐藏符号属性”原则的一部分。如果另一个脚本或库遍历我们的对象，它不会意外地访问到符号属性。

相反，Object.assign 会同时复制字符串和 symbol 属性：

```js
let id = Symbol("id");
let user = {
  [id]: 123
};

let clone = Object.assign({}, user);

alert( clone[id] ); // 123
```

## Creating symbols

ES6 添加了 Symbol 作为新的原始类型。与其他基本类型（例如 number、boolean、null、undefined 和 string）不同，symbol 类型没有字面量形式。

To create a new symbol, you use the global `Symbol()` function as shown in this example:

```js
let s = Symbol('foo');
```

The `Symbol()` function creates a new *unique* value each time you call it:

```js
console.log(Symbol() === Symbol()); // false
```

The `Symbol()` function accepts a `description` (string or number) as an optional argument. The `description` argument will make your symbol more descriptive.

The following example creates two symbols: `firstName` and `lastName`.

```js
let firstName = Symbol('first name'),
    lastName = Symbol('last name');
```

You can access the symbol’s description property using the `toString()` method. The `console.log()` method calls the `toString()` method of the symbol implicitly as shown in the following example:

```js
console.log(firstName); // Symbol(first name)
console.log(lastName); // Symbol(last name)
```

Since symbols are primitive values, you can use the  `typeof` operator to check whether a variable is a symbol. ES6 extended `typeof` to return the `symbol` string when you pass in a symbol variable:

```js
console.log(typeof firstName); // symbol
```

## Sharing symbols

ES6 provides you with a global symbol registry that allows you to share symbols globally.If you want to create a symbol that will be shared, you use the `Symbol.for()` method instead of calling the `Symbol()` function.

The `Symbol.for()` method accepts a single parameter that can be used for symbol’s description, as shown in the following example:

```js
let ssn = Symbol.for('ssn');
```

The `Symbol.for()` method first searches for the symbol with the  `ssn` key in the global symbol registry. It returns the existing symbol if there is one. Otherwise, the `Symbol.for()` method creates a new symbol, registers it to the global symbol registry with the specified key, and returns the symbol.

Later, if you call the `Symbol.for()` method using the same key, the `Symbol.for()` method will return the existing symbol.

```js
let citizenID = Symbol.for('ssn');
console.log(ssn === citizenID); // true
```

To get the key associated with a symbol, you use the `Symbol.keyFor()` method as shown in the following example:

```js
console.log(Symbol.keyFor(citizenID)); // 'ssn'
```

If a symbol does not exist in the global symbol registry, the `Symbol.keyFor()` method returns `undefined`.

```js
let systemID = Symbol('sys');
console.log(Symbol.keyFor(systemID)); // undefined
```

## Symbol usages

### Using symbols as unique values

Whenever you use a string or a number in your code, you should use symbols instead. For example, you have to manage the status in the task management application.

Before ES6, you would use strings such as `open`, `in progress`, `completed`, `canceled`, and `on hold` to represent different statuses of a task. In ES6, you can use symbols as follows:

```js
let statuses = {
    OPEN: Symbol('Open'),
    IN_PROGRESS: Symbol('In progress'),
    COMPLETED: Symbol('Completed'),
    HOLD: Symbol('On hold'),
    CANCELED: Symbol('Canceled')
};
// complete a task
task.setStatus(statuses.COMPLETED);
```

### Using a symbol as the computed property name of an object

You can use symbols as computed property names.

```js
let status = Symbol('status');
let task = {
    [status]: statuses.OPEN,
    description: 'Learn ES6 Symbol'
};
console.log(task);
```

To get all the enumerable properties of an object, you use the `Object.keys()` method.

```js
console.log(Object.keys(task)); // ["description"]
```

To get all properties of an object whether the properties are enumerable or not, you use the `Object.getOwnPropertyNames()` method.

```js
console.log(Object.getOwnPropertyNames(task)); // ["description"]
```

To get all property symbols of an object, you use the `Object.getOwnPropertySymbols()` method, which has been added in ES6.

```js
console.log(Object.getOwnPropertySymbols(task)); // [Symbol(status)]
```

The `Object.getOwnPropertySymbols()` method returns an array of own property symbols from an object.

symbol 有两个主要的使用场景：

1. “隐藏” 对象属性。

   如果我们想要向“属于”另一个脚本或者库的对象添加一个属性，我们可以创建一个 symbol 并使用它作为属性的键。symbol 属性不会出现在 `for..in` 中，因此它不会意外地被与其他属性一起处理。并且，它不会被直接访问，因为另一个脚本没有我们的 symbol。因此，该属性将受到保护，防止被意外使用或重写。

   因此我们可以使用 symbol 属性“秘密地”将一些东西隐藏到我们需要的对象中，但其他地方看不到它。

2. JavaScript 使用了许多系统 symbol，这些 symbol 可以作为 `Symbol.*` 访问。我们可以使用它们来改变一些内建行为。例如，我们将使用 `Symbol.iterator` 来进行 迭代 操作，使用 `Symbol.toPrimitive` 来设置 对象原始值的转换 等等

## Well-known symbols

ES6 provides predefined symbols which are called well-known symbols. The well-known symbols represent the common behaviors in JavaScript. Each well-known symbol is a static property of the `Symbol` object.

### Symbol.hasInstance

The `Symbol.hasInstance` is a symbol that changes the behavior of the `instanceof` operator. Typically, when you use the `instanceof` operator:

```js
obj instanceof type;
```

JavaScript will call the `Symbol.hasIntance` method as follows:

```js
type[Symbol.hasInstance](obj);
```

It then depends on the method to determine if `obj` is an instance of the `type` object.

```js
class Stack {
}
console.log([] instanceof Stack); // false
```

The `[]` array is not an instance of the `Stack` class, therefore, the `instanceof` operator returns `false` in this example.

Assuming that you want the `[]` array is an instance of the `Stack` class, you can add the `Symbol.hasInstance` method as follows:

```js
class Stack {
    static [Symbol.hasInstance](obj) {
        return Array.isArray(obj);
    }
}
console.log([] instanceof Stack); // true
```

### Symbol.iterator

The `Symbol.iterator` specifies whether a function will return an iterator for an object.

The objects that have `Symbol.iterator` property are called iterable objects.

In ES6, all collection objects (Array, Set and Map) and strings are iterable objects.

ES6 provides the for…of loop that works with the iterable object as in the following example.

```js
var numbers = [1, 2, 3];
for (let num of numbers) {
    console.log(num);
}

// 1
// 2
// 3
```

Internally, the JavaScript engine first calls the `Symbol.iterator` method of the numbers array to get the iterator object.

Then, it invokes the `iterator.next()` method to return a result object with two properties `value` and `done`, and copies the value property into the `num ` variable.

After three iterations, the `done` property of the result object is `true`, the loop exits.

You can access the default iterator object via `System.iterator` symbol as follows:

```js
var iterator = numbers[Symbol.iterator]();

console.log(iterator.next()); // Object {value: 1, done: false}
console.log(iterator.next()); // Object {value: 2, done: false}
console.log(iterator.next()); // Object {value: 3, done: false}
console.log(iterator.next()); // Object {value: undefined, done: true}
```

By default, a collection is not iterable. However, you can make it iterable by using the `Symbol.iterator` as shown in the following example:

```js
class List {
    constructor() {
        this.elements = [];
    }

    add(element) {
        this.elements.push(element);
        return this;
    }

    *[Symbol.iterator]() {
        for (let element of this.elements) {
            yield  element;
        }
    }
}

let chars = new List();
chars.add('A')
     .add('B')
     .add('C');

// because of the Symbol.iterator
for (let c of chars) {
    console.log(c);
}

// A
// B
// C
```

### Symbol.isConcatSpreadable

To concatenate two arrays, you use the `concat()` method as shown in the following example:

```js
let odd  = [1, 3],
    even = [2, 4];
let all = odd.concat(even);
console.log(all); // [1, 3, 2, 4]
```

在此示例中，生成的数组包含两个数组的单个元素。此外，concat() 方法还接受非数组参数，如下所示。

```js
let extras = all.concat(5);
console.log(extras); // [1, 3, 2, 4, 5]
```

数字 5 成为数组的第五个元素。

当我们将数组传递给 concat() 方法时，concat() 方法将数组分散为各个元素。然而，它以不同的方式对待单个原始参数（primitive argument）。在 ES6 之前，无法更改此行为。

这就是 Symbol.isConcatSpread 符号发挥作用的原因。

Symbol.isConcatSpread 属性是一个布尔值，用于确定是否将对象单独添加到 concat() 函数的结果中。

考虑以下示例：

```js
let list = {
    0: 'JavaScript',
    1: 'Symbol',
    length: 2
};
let message = ['Learning'].concat(list);
console.log(message); // [ 'Learning', { '0': 'JavaScript', '1': 'Symbol', length: 2 } ]
```

The list object is concatenated to the `['Learning']` array. However, its individual elements are not spreaded.

To enable the elements of the `list` object added to the array individually when passing to the `concat()` method, you need to add the `Symbol.isConcatSpreadable` property to the `list` object as follows:

```js
let list = { // array-like object
    0: 'JavaScript',
    1: 'Symbol',
    length: 2,
    [Symbol.isConcatSpreadable]: true
};
let message = ['Learning'].concat(list);
console.log(message); // ["Learning", "JavaScript", "Symbol"]
```

### Symbol.toPrimitive

The `Symbol.toPrimitive` method determines what should happen when an object is converted into a primitive value.

The JavaScript engine defines the `Symbol.toPrimitive` method on the prototype of each standard type.

The `Symbol.toPrimitive` method takes a `hint` argument that has one of three values: “number”, “string”, and “default”. The `hint` argument specifies the type of the return value. The `hint` parameter is filled by the JavaScript engine based on the context in which the object is used.

Here is an example of using the `Symbol.toPrimitive` method.

```js
function Money(amount, currency) {
    this.amount = amount;
    this.currency = currency;
}

Money.prototype[Symbol.toPrimitive] = function(hint) {
    let result;
    switch (hint) {
        case 'string':
            result = this.amount + this.currency;
            break;
        case 'number':
            result = this.amount;
            break;
        case 'default':
            result = this.amount + this.currency;
            break;
    }
    return result;
}

let price = new Money(799, 'USD');

console.log('Price is ' + price); // Price is 799USD
console.log(+price + 1); // 800
console.log(String(price)); // 799USD
```