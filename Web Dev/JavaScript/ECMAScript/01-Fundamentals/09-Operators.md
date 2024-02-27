# Operators

## Arithmetic Operators

### Addition operator (+)

如果任一值是字符串，则加法运算符使用以下规则：

- 如果两个值都是字符串，则它将第二个字符串连接到第一个字符串。 

- 如果一个值是字符串，它会隐式地将数值转换为字符串并连接两个字符串。

```js
let x = '10',
    y = '20';
let result = x + y;
console.log(result); // 1020
```

```js
let result = 10 + '20';
console.log(result); // 1020
```

### Subtraction operator (-)

如果值是 string、boolean、null 或 undefined，JavaScript 引擎将： 

- 首先，使用 Number() 函数将值转换为数字。 
- 其次，进行减法。

### Multiplication operator (*)

JavaScript 使用星号 (*) 来表示乘法运算符。乘法运算符将两个数字相乘并返回一个值。

如果任一值都不是数字，JavaScript 引擎会使用 Number() 函数将其隐式转换为数字并执行乘法。例如：

```js
let result = 2 * 3;
console.log(result); // 6

let result = '5' * 2;
console.log(result); // 10
```

### Divide operator (/)

Javascript 使用斜杠 (/) 字符来表示除法运算符。除法运算符将第一个值除以第二个值。

如果其中一个值不是数字，JavaScript 引擎会将其转换为数字以进行除法。例如：

```js
let result = '20' / 2;
console.log(result); // 10;
```

### Using JavaScript arithmetic operators with objects

如果一个值是一个对象，JavaScript 引擎会调用该对象的 valueOf() 方法来获取该值进行计算。

```js
let energy = {
  valueOf() {
    return 100;
  },
};
let currentEnergy = energy - 10;
console.log(currentEnergy); // 90
currentEnergy = energy + 100;
console.log(currentEnergy); // 200
currentEnergy = energy / 2;
console.log(currentEnergy); // 50
currentEnergy = energy * 1.5;
console.log(currentEnergy); // 150
```

如果对象没有 valueOf() 方法，但有 toString() 方法，JavaScript 引擎将调用 toString() 方法来获取值进行计算。

```js
let energy = {
  toString() {
    return 50;
  },
};
let currentEnergy = energy - 10;
console.log(currentEnergy);
currentEnergy = energy + 100;
console.log(currentEnergy);
currentEnergy = energy / 2;
console.log(currentEnergy);
currentEnergy = energy * 1.5;
console.log(currentEnergy);
```

## Remainder Operator

JavaScript 使用 % 来表示余数运算符。余数运算符返回一个值除以另一个值时剩下的余数。

如果被除数或除数不是数字，则使用 Number() 函数将其转换为数字并应用上述规则。

## Assignment Operators

赋值运算符 (=) 将值赋给变量。

### Chaining JavaScript assignment operators

```js
let a = 10, b = 20, c = 30;
a = b = c; // all variables are 30
```

在此示例中，JavaScript 从右到左进行计算。因此，它执行以下操作：

```js
let a = 10, b = 20, c = 30;

b = c; // b is 30
a = b; // a is also 30 
```

## Unary Operators

一元运算符作用于一个值。下表显示一元运算符及其含义：

| Unary Operators | Name                         | Meaning                                     |
| :-------------- | :--------------------------- | :------------------------------------------ |
| +x              | Unary Plus                   | Convert a value into a number               |
| -x              | Unary Minus                  | Convert a value into a number and negate it |
| ++x             | Increment Operator (Prefix)  | Add one to the value                        |
| –-x             | Decrement Operator (Prefix)  | Subtract one from the value                 |
| x++             | Increment Operator (Postfix) | Add one to the value                        |
| x–-             | Decrement Operator (Postfix) | Subtract one from the value                 |

### Unary plus (+)

一元加运算符是一个简单的加号 (+)。如果将一元加号放在数值之前，则不会执行任何操作。

当将一元加运算符应用于非数字值时，它会使用 Number() 函数按照下表中的规则执行数字转换：

| Value     | Result                                                       |
| :-------- | :----------------------------------------------------------- |
| boolean   | `false` to `0`, `true` to `1`                                |
| string    | Convert the string value based on a set of specific rules    |
| object    | Call the `valueOf()` and/or `toString()` method to get the value to convert into a number |
| null      | 0                                                            |
| undefined | NaN                                                          |

```js
let s = '10';
console.log(+s); // 10

let f = false,
    t = true;
console.log(+f); // 0
console.log(+t); // 1

let person = {
  name: 'John',
  toString: function () {
    return '25';
  },
};
console.log(+person); // 25

let person = {
  name: 'John',
  toString: function () {
    return '25';
  },
  valueOf: function () {
    return '30';
  },
};
console.log(+person); // 30
```

### Unary minus (-)

一元减号运算符是单个减号 (-)。如果将一元减运算符应用于数字，则会对该数字求负。例如：

```js
let x = 10;
let y = -x;

console.log(y); // -10
```

如果将一元减运算符应用于非数字值，它会使用与一元加运算符相同的规则将该值转换为数字，然后对该值求反。

## Increment / Decrement operators

增量运算符有两个加号 (++)，减量运算符有两个减号 (--)。

自增和自减运算符都有两个版本：前缀和后缀。

前缀递增或递减运算符在计算语句前更改值。

后缀递增或递减运算符在计算语句后更改值。

## Comparison Operators

`> >= < <= == === != !==`

A comparison operator returns a Boolean value indicating whether the comparison is true or not. See the following example:

```js
let r1 = 20 > 10; // true
let r2 = 20 < 10; // false
let r3 = 10 == 10; // true
```

比较运算符采用两个值。如果值的类型不可比较，则比较运算符根据特定规则将它们转换为可比较类型的值。

对不同类型的值进行相等检查时，运算符 `==` 会将不同类型的值转换为数字（除了 `null` 和 `undefined`，它们彼此相等而没有其他情况）。

其他比较也将转换为数字。

严格相等运算符 `===` 不会进行转换：不同的类型总是指不同的值。

值 `null` 和 `undefined` 是特殊的：它们只在 `==` 下相等，且不相等于其他任何值。

NaN 不等于任何值包括它本身，可以使用 `Number.isNaN()` 方法比较是否为 `NaN`。

大于/小于比较，在比较字符串时，会按照字符顺序逐个字符地进行比较。其他类型则被转换为数字。

### Compare numbers

If values are numbers, the comparison operators perform a numeric comparison.

```js
let a = 10, 
    b = 20; 

console.log(a >= b);  // false
console.log(a == 10); // true
```

### Compare strings

如果操作数是字符串，JavaScript 会按照数字方式对字符串中的字符代码（Unicode code point）进行一一比较。

```js
let name1 = 'alice',
    name2 = 'bob';    

let result = name1 < name2;
console.log(result); // true
console.log(name1 == 'alice'); // true
```

### Compare a number with a value of another type

如果一个值是数字而另一个不是数字，则比较运算符会将非数字值转换为数字，然后对它们进行数字比较。

```js
console.log(10 < '20'); // true
```

### Compare an object with a non-object

如果值是对象，则调用该对象的 valueOf() 方法以返回值进行比较。如果对象没有 valueOf() 方法，则会调用 toString() 方法。

```js
let apple = {
  valueOf: function () {
    return 10;
  },
};

let orange = {
  toString: function () {
    return '20';
  },
};
console.log(apple > 10); // false
console.log(orange == 20); // true
```

### Compare a Boolean with another value

如果某个值是布尔值，JavaScript 会将其转换为数字，并将转换后的值与其他值进行比较； true 转换为 1，false 转换为 0。

除了上述规则外，等于（==）和不等于（!=）运算符还有以下规则。

### Compare `null` and `undefined`

在 JavaScript 中，null 等于 undefined。这意味着以下表达式返回 true。

```js
console.log(null == undefined); // true
```

### Compare `NaN` with other values

如果任一值为 NaN，则等于运算符 (==) 返回 false。

```js
console.log(NaN == 1); // false
console.log(NaN === NaN); // false
```

### Strict equal (`===`) and not strict equal (`!==`)

严格等于和非严格等于运算符的行为类似于等于和不等于运算符，只不过它们在比较之前不转换操作数。

```js
console.log("10" == 10); // true
console.log("10" === 10); // false
```

在第一个比较中，由于使用了相等运算符，JavaScript 将字符串转换为数字并执行比较。

然而，在第二次比较中，使用了严格等于运算符（ ===），JavaScript 在比较之前不会转换字符串，因此结果为 false。

## Logical Operators

JavaScript 提供了三种逻辑运算符： 

- &&
- ||
- !

### The Logical NOT operator (!)

JavaScript 使用感叹号 ! 来表示逻辑 NOT 运算符。! 运算符可以应用于任何类型的单个值，而不仅仅是布尔值。

When you apply the `!` operator to a boolean value, the `!` returns `true` if the value is `false` and vice versa.

```js
let eligible = false,
    required = true;

console.log(!eligible); // true
console.log(!required); // false
```

When you apply the ! operator to a non-Boolean value. The ! operator first converts the value to a boolean value and then negates it.

```js
console.log(!undefined); // true
console.log(!null); // true
console.log(!20); //false
console.log(!0); //true
console.log(!NaN); //true
console.log(!{}); // false
console.log(!''); //true
console.log(!'OK'); //false
console.log(!false); //true
console.log(!true); //false
```

#### Double-negation (`!!`)

The `!!` uses the logical NOT operator (`!`) twice to convert a value to its real boolean value.

The result is the same as using the Boolean() function.

```js
let counter = 10;
console.log(!!counter); // true
```

### The Logical AND operator (`&&`)

JavaScript uses the double ampersand (`&&`) to represent the logical AND operator. The following expression uses the `&&` operator:

```js
let result = a && b;
```

如果 a 可以转换为 true，&& 运算符返回 b；否则，返回 a。事实上，这条规则适用于所有布尔值。

#### Short-circuit evaluation

&& 运算符被短路。这意味着仅当第一个值不足以确定表达式的值时，&& 运算符才会计算第二个值。

```js
let b = true;
let result = b && (1 / 0);
console.log(result); // Infinity
```

在此示例中，b 为 true，因此 && 运算符在不进一步计算第二个表达式 (1/0) 的情况下无法确定结果。

结果是 Infinity，即表达式 (1/0) 的结果。然而：

```js
let b = false;
let result = b && (1 / 0);
console.log(result); // false
```

在这种情况下，b 为 false，&& 运算符不需要计算第二个表达式，因为它可以将最终结果确定为第一个变量的基于 false 的值。

#### The chain of `&&` operators

```js
let result = value1 && value2 && value3;
```

The `&&` operator carries the following:

- Evaluates values from left to right.
- For each value, convert it to a boolean. If the result is `false`, stops and returns the original value.
- If all values are **truthy values**, return the last value.

In other words, The `&&` operator returns the first falsy value or the last value if none were found.

> If a value can be converted to `true`, it is so-called a truthy value. If a value can be converted to `false`, it is a so-called falsy value.

### The Logical OR operator (`||`)

JavaScript uses the double pipe `||` to represent the logical OR operator. You can apply the `||` operator to two values of any type:

```js
let result = a || b;
```

If `a` can be converted to `true`, returns `a`; else, returns `b`. This rule is also applied to boolean values.

The `||` operator returns `false` if both values evaluate to `false`. In case either value is `true`, the `||` operator returns `true`.

```js
let eligible = true,
    required = false;

console.log(eligible || required); // true
```

#### The `||` operator is also short-circuited

Similar to the `&&` operator, the `||` operator is short-circuited. It means that if the first value evaluates to `true`, the `&&` operator doesn’t evaluate the second one.

#### The chain of `||` operators

```js
let result = value1 || value2 || value3;
```

The `||` operator does the following:

- Evaluates values from left to right.
- For each value, converts it to a boolean value. If the result of the conversion is `true`, stops and returns the original value.
- If all values have been evaluated to `false`, returns the last value.

In other words, the chain of the `||` operators returns the first truthy value or the last one if no truthy value was found.

## Exponentiation Operator

static method `Math.pow()`:

```js
Math.pow(base, exponent)
```

ECMAScript 2016 provided an alternative way to get a base to the exponent power by using the exponentiation operator ( `**`) with the following syntax:

```js
x**n
```

JavaScript does not allow you to put a unary operator immediately before the base number. If you attempt to do so, you’ll get a `SyntaxError`.

The following example causes a syntax error:

```js
let result = -2**3;
Uncaught SyntaxError: Unary operator used immediately before exponentiation expression. Parenthesis must be used to disambiguate operator precedence
```

To fix this, you use parentheses like this:

```js
let result = (-2)**3;
console.log(result); // -8
```

## Ternary Operator (?:)

### Introduction to JavaScript ternary operator

In this example, we show a message that a person can drive if the age is greater than or equal to 16. Alternatively, you can use a ternary operator instead of the if-else statement like this:

```js
let age = 18;
let message;
age >= 16 ? (message = 'You can drive.') : (message = 'You cannot drive.');
console.log(message); // You can drive.
```

Or you can use the ternary operator in an expression as follows:

```js
let age = 18;
let message;
message = age >= 16 ? 'You can drive.' : 'You cannot drive.';
console.log(message);
```

Here’s the syntax of the ternary operator:

```js
condition ? expressionIfTrue : expressionIfFalse;
```

In this syntax, the `condition` is an expression that evaluates to a Boolean value, either `true` or `false`.

If the condition is `true`, the first expression (`expresionIfTrue`) executes. If it is false, the second expression (`expressionIfFalse`) executes.

The following shows the syntax of the ternary operator used in an expression:

```js
let variableName = condition ? expressionIfTrue : expressionIfFalse;
```

### JavaScript ternary operator examples

#### Using multiple JavaScript ternary operators example

The following example shows how to use two ternary operators in the same expression:

```js
let speed = 90;
let message = speed >= 120 ? 'Too Fast' : speed >= 80 ? 'Fast' : 'OK';

console.log(message); // Fast
```

It’s a good practice to use the ternary operator when it makes the code easier to read. If the logic contains many `if...else` statements, you should avoid using the ternary operators.

## JavaScript instanceof

### Introduction to the JavaScript instanceof operator

如果构造函数的原型 (constructor.prototype) 出现在对象的原型链中，instanceof 运算符将返回 true。

下面显示了 instanceof 运算符的语法：

```js
object instanceof contructor
```

在这个语法中：

- object 是要测试的对象。
- 构造函数是一个要测试的函数。

以下示例定义了 Person 类型并使用 instanceof 运算符来检查对象是否是该类型的实例：

```js
function Person(name) {
  this.name = name;
}

let p1 = new Person('John');

console.log(p1 instanceof Person); // true
```

它返回 true，因为 Person.prototype 出现在 p1 对象的原型链上。 p1 的原型链是 p1、Person.prototype 和 Object.prototype 之间的链接：

<img src="https://www.javascripttutorial.net/wp-content/uploads/2022/01/JavaScript-instanceof.svg" alt="img" style="zoom:80%;" />

以下也返回 true，因为 Object.prototype 出现在 p1 对象的原型链上：

```js
console.log(p1 instanceof Object); // true
```

### ES6 class and instanceof operator

以下示例定义了 Person 类并使用 instanceof 运算符来检查对象是否是该类的实例：

```js
class Person {
  constructor(name) {
    this.name = name;
  }
}

let p1 = new Person('John');

console.log(p1 instanceof Person); // true
```

### The instanceof operator and inheritance

以下示例定义了扩展 Person 类的 Employee 类：

```javascript
class Person {
  constructor(name) {
    this.name = name;
  }
}

class Employee extends Person {
  constructor(name, title) {
    super(name);
    this.title = title;
  }
}

let e1 = new Employee();

console.log(e1 instanceof Employee); // true
console.log(e1 instanceof Person); // true
console.log(e1 instanceof Object); // true
```

由于 e1 是 Employee 类的实例，因此它也是 Person 和 Object 类（基类）的实例。

### Symbol.hasInstance

在 ES6 中，instanceof 运算符使用 Symbol.hasInstance 函数来检查关系。Symbol.hasInstance() 接受一个对象，如果类型将该对象作为实例，则返回 true。

```js
class Person {
  constructor(name) {
    this.name = name;
  }
}

let p1 = new Person('John');
typeof Symbol.hasInstance // symbol
console.log(Person[Symbol.hasInstance](p1)); // true
```

由于 Symbol.hasInstance 是在 Function 原型上定义的，因此默认情况下它在所有函数和类中自动可用。

可以将子类上的 Symbol.hasInstance 重新定义为静态方法。例如：

```js
class Person {
  constructor(name) {
    this.name = name;
  }
}

class Android extends Person {
  static [Symbol.hasInstance]() {
    return false;
  }
}

let a1 = new Android('Sonny');

console.log(a1 instanceof Android); // false
console.log(a1 instanceof Person); // false
```
