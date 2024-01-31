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

console.log(result);
1020
```

```js
let result = 10 + '20';

console.log(result);
1020
```

下表显示了对特殊数字使用加法运算符时的结果：

### Subtraction operator (-)

如果值是字符串、布尔值、null 或未定义，JavaScript 引擎将： 

- 首先，使用 Number() 函数将值转换为数字。 
- 其次，进行减法。

### Multiplication operator (*)

JavaScript 使用星号 (*) 来表示乘法运算符。乘法运算符将两个数字相乘并返回一个值。

如果任一值都不是数字，JavaScript 引擎会使用 Number() 函数将其隐式转换为数字并执行乘法。例如：

```js
let result = 2 * 3;
console.log(result);
6

let result = '5' * 2;
console.log(result);
10
```

### Divide operator (/)

Javascript 使用斜杠 (/) 字符来表示除法运算符。除法运算符将第一个值除以第二个值。

如果其中一个值不是数字，JavaScript 引擎会将其转换为数字以进行除法。例如：

```js
let result = '20' / 2;
console.log(result); // 10;
```

### Using JavaScript arithmetic operators with objects

如果一个值是一个对象，JavaScript引擎会调用该对象的valueOf()方法来获取该值进行计算。例如：

```js
let energy = {
  valueOf() {
    return 100;
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

// 输出
90
200
50
150
```

如果对象没有 valueOf() 方法，但有 toString() 方法，JavaScript 引擎将调用 toString() 方法来获取值进行计算。例如：

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

// 输出
40
150
25
75
```

## Remainder Operator

JavaScript 使用 % 来表示余数运算符。余数运算符返回一个值除以另一个值时剩下的余数。

如果被除数或除数不是数字，则使用 Number() 函数将其转换为数字并应用上述规则。

## Assignment Operators

赋值运算符 (=) 将值赋给变量。

下表说明了赋值运算符，它们是另一个运算符和赋值的简写：

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
| –x              | Decrement Operator (Prefix)  | Subtract one from the value                 |
| x++             | Increment Operator (Postfix) | Add one to the value                        |
| x–              | Decrement Operator (Postfix) | Subtract one from the value                 |

### Unary plus (+)

一元加运算符是一个简单的加号 (+)。如果将一元加号放在数值之前，则不会执行任何操作。

当将一元加运算符应用于非数字值时，它会使用 Number() 函数按照下表中的规则执行数字转换：

| Value   | Result                                                       |
| :------ | :----------------------------------------------------------- |
| boolean | `false` to `0`, `true` to `1`                                |
| string  | Convert the string value based on a set of specific rules    |
| object  | Call the `valueOf()` and/or `toString()` method to get the value to convert into a number |

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

自增和自减运算符都有两个版本：前缀和后缀。您可以将增量或减量运算符的前缀和后缀版本放置在它们所应用的变量之前和之后。

前缀递增或递减运算符在计算语句前更改值。

后缀递增或递减运算符在计算语句后更改值。

## Comparison Operators

A comparison operator returns a Boolean value indicating whether the comparison is true or not. See the following example:

```js
let r1 = 20 > 10; // true
let r2 = 20 < 10; // false
let r3 = 10 == 10; // true
```

比较运算符采用两个值。如果值的类型不可比较，则比较运算符根据特定规则将它们转换为可比较类型的值。

### Compare numbers

If values are numbers, the comparison operators perform a numeric comparison. For example:

```js
let a = 10, 
    b = 20; 

console.log(a >= b);  // false
console.log(a == 10); // true
```

### Compare strings

如果操作数是字符串，JavaScript 会按照数字方式对字符串中的字符代码（Unicode 马店）进行一一比较。

```js
let name1 = 'alice',
    name2 = 'bob';    

let result = name1 < name2;
console.log(result); // true
console.log(name1 == 'alice'); // true
```

### Compare a number with a value of another type

如果一个值是数字而另一个不是数字，则比较运算符会将非数字值转换为数字，然后对它们进行数字比较。例如：

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

在第一个比较中，由于我们使用了相等运算符，JavaScript 将字符串转换为数字并执行比较。

然而，在第二次比较中，我们使用了严格等于运算符（ ===），JavaScript 在比较之前不会转换字符串，因此结果为 false。

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

The result is the same as using the Boolean() function. For example:

```js
let counter = 10;
console.log(!!counter); // true
```

### The Logical AND operator (`&&`)

JavaScript uses the double ampersand (`&&`) to represent the logical AND operator. The following expression uses the `&&` operator:

```js
let result = a && b;
```

如果a可以转换为true，&&运算符返回b；否则，返回 a。事实上，这条规则适用于所有布尔值。

#### Short-circuit evaluation

&& 运算符被短路。这意味着仅当第一个值不足以确定表达式的值时，&& 运算符才会计算第二个值。例如：

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
- If all values are truthy values, return the last value.

In other words, The `&&` operator returns the first falsy value or the last value if none were found.

> If a value can be converted to `true`, it is so-called a truthy value. If a value can be converted to `false`, it is a so-called falsy value.

### The Logical OR operator (`||`)

JavaScript uses the double pipe `||` to represent the logical OR operator. You can apply the `||` operator to two values of any type:

```js
let result = a || b;
```

If `a` can be converted to `true`, returns `a`; else, returns `b`. This rule is also applied to boolean values.

The `||` operator returns `false` if both values evaluate to `false`. In case either value is `true`, the `||` operator returns `true`. For example:

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

### Logical operator precedence

当您在表达式中混合逻辑运算符时，JavaScript 引擎会根据指定的顺序计算运算符。这种顺序称为运算符优先级。

The precedence of the logical operator is in the following order from the highest to the lowest:

1. Logical NOT (!)
2. Logical AND (&&)
3. Logical OR (||)

## Logical Assignment Operators

ES2021 introduces three logical assignment operators including:

- Logical OR assignment operator (`||=`)
- Logical AND assignment operator (`&&=`)
- Nullish coalescing assignment operator (`??=`)

The following table shows the equivalent of the logical assignments operator:

| Logical Assignment Operators | Logical Operators |
| :--------------------------- | :---------------- |
| x \|\|= y                    | x \|\| (x = y)    |
| x &&= y                      | x && (x = y)      |
| x ??= y                      | x ?? (x = y);     |

### The Logical OR assignment operator

The logical OR assignment operator (`||=`) accepts two operands and assigns the right operand to the left operand if the left operand is falsy:

```js
x ||= y
```

In this syntax, the `||=` operator only assigns `y` to `x` if `x` is falsy. For example:

```js
let title;
title ||= 'untitled';

console.log(title); // untitled
```

```js
let title = 'JavaScript Awesome';
title ||= 'untitled';

console.log(title); // JavaScript Awesome
```

Like the logical OR operator, the logical OR assignment also short-circuits. It means that the logical OR assignment operator only performs an assignment when the `x` is falsy.

The following example uses the logical assignment operator to display a default message if the search result element is empty:

```js
document.querySelector('.search-result').textContent ||= 'Sorry! No result found';
```

### The Logical AND assignment operator

The logical AND assignment operator only assigns `y` to `x` if `x` is truthy:

```js
x &&= y;
```

The logical AND assignment operator also short-circuits. It means that

```js
x &&= y;
```

is equivalent to:

```js
x && (x = y);
```

The following example uses the logical AND assignment operator to change the last name of a `person` object if the last name is truthy:

```js
let person = {
    firstName: 'Jane',
    lastName: 'Doe',
};

person.lastName &&= 'Smith';

console.log(person); // {firstName: 'Jane', lastName: 'Smith'}
```

### The nullish coalescing assignment operator

如果 x 为 null 或 undefined，则 nullish 合并赋值运算符仅将 y 赋值给 x：

```js
x ??= y;
```

It’s equivalent to the following statement that uses the nullish coalescing operator:

```js
x ?? (x = y);
```

The following example uses the nullish coalescing assignment operator to add a missing property to an object:

```js
let user = {
    username: 'Satoshi'
};
user.nickname ??= 'anonymous';

console.log(user); // {username: 'Satoshi', nickname:'anonymous'}
```

## Nullish Coalescing Operator

### Introduction to the JavaScript nullish coalescing operator

ES2020 引入了用双问号 (??) 表示的空合并运算符。空合并运算符是一个接受两个值的逻辑运算符：

```js
value1 ?? value2
```

The nullish coalescing operator returns the second value (`value2`) if the first value (`value2`) is `null` or `undefined`. Technically, the nullish coalescing operator is equivalent to the following block:

```js
const result = value1;
if(result === null || result === undefined) {
   result = value2;
}
```

> A nullish value is a value that is either `null` or `undefined`.

```js
const name = null ?? 'John';
console.log(name); // 'John'
```

### The nullish coalescing operator is short-circuited

Similar to the logical OR and AND operators, the nullish coalescing operator does not evaluate the second value if the first operand is neither undefined nor null.

```js
let result = 1 ?? console.log('Hi');
```

In this example, the operator `??` does not evaluate the second expression that displays the “Hi” to the console because the first value is `1`, which is not `null` or `undefined`.

### Chaining with the AND or OR operator

A `SyntaxError` will occur if you combine the logical AND or OR operator directly with the nullish coalescing operator like this:

```js
const result = null || undefined ?? 'OK'; // SyntaxError
```

However, you can avoid this error by wrapping the expression on the left of the `??` operator in parentheses to explicitly specify the operator precedences:

```js
const result = (null || undefined) ?? 'OK'; 
console.log(result); // 'OK'
```

## Exponentiation Operator

static method `Math.pow()`

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
```

```js
Uncaught SyntaxError: Unary operator used immediately before exponentiation expression. Parenthesis must be used to disambiguate operator precedence
```

To fix this, you use parentheses like this:

```js
let result = (-2)**3;
console.log(result); // -8
```

## Object Spread

在 ES6 中，可以使用扩展运算符 (...) 来解包数组的元素。ES2018 扩展了展开运算符 (...)，使其能够与对象自身的可枚举属性一起使用。假设您有一个具有一个属性 radius 的 circle 对象：

```js
const circle = {
    radius: 10
};
```

以下示例使用展开运算符 (...) 创建一个 colorCircle 对象，该对象具有 circle 对象的所有属性以及一个附加属性 color：

```js
const coloredCircle = {
    ...circle,
    color: 'black'
};
console.log(coloredCircle);
// 输出
{
    radius: 10,
    color: 'black'
}
```

### JavaScript Object spread operator use cases

#### clone an object

可以使用扩展运算符来克隆对象自己的**可枚举**属性：

```js
const circle = {
    radius: 10
};

const clonedCircle = {...circle};

console.log(clonedCircle); // { radius: 10 }
```

请注意，克隆始终是浅克隆。

```js
const circle = {
    radius: 10,
    style: {
        color: 'blue'
    }
};
const clonedCircle = {
    ...circle
};
circle.style.color = 'red';
console.log(clonedCircle.style.color); // red
```

#### Merging objects

```js
const circle = {
    radius: 10
};
const style = {
    backgroundColor: 'red'
};
const solidCircle = {
    ...circle,
    ...style
};
console.log(solidCircle); // { radius: 10, backgroundColor: 'red' }
```

### Spread operator vs. `Object.assign()`

展开运算符 (...) 在目标对象中定义新属性，而 Object.assign() 方法则对它们进行分配。它有两个副作用。

#### Target objects with setters

Object.assign() 调用目标对象上的 setter，而展开运算符则不会。

```js
class Circle {
    constructor(radius) {
        this.radius = radius;
    }
    set diameter(value) {
        this.radius = value / 2;
        console.log('SET ', value);
    }
    get diameter() {
        return this.radius * 2;
    }
}

let circle = new Circle(100);
let cloneCircle1 = Object.assign(circle, {
    diameter: 200
});
let cloneCircle2 = {
    ...circle
};
// 输出
SET  200
```

#### Target objects with read-only properties

如果目标对象具有只读属性，则无法使用 Object.assign() 方法为该属性分配新值。但是，展开运算符 (...) 可以定义新属性。假设您有一个名为 blueSquare 的对象，其颜色属性是只读的：

```js
const blueSquare = {
    length: 100,
    color: 'blue'
};

Object.defineProperty(blueSquare, 'color', {
    value: 'blue',
    enumerable: true,
    writable: false

});

console.log(blueSquare); // { length: 100, color: 'blue' }
```

下面使用展开运算符 (...) 来合并style和 blueSquare 对象：

```js
// merge style and blueSquare objects:
const style = {
    color: 'green'
};

const greenSquare = {
    ...blueSquare,
    ...style
};

console.log(greenSquare); // { length: 100, color: 'green' }
```

然而，如果你使用Object.assign()方法，你会得到一个错误：

```js
// merge style and redSquare objects: ERROR
const redSquare = Object.assign(blueSquare, {
    color: 'red'
});
TypeError: Cannot assign to read only property 'color' of object '#<Object>'
```

## Ternary Operator (:?)

### Introduction to JavaScript ternary operator

In this example, we show a message that a person can drive if the age is greater than or equal to 16. Alternatively, you can use a ternary operator instead of the if-else statement like this:

```js
let age = 18;
let message;

age >= 16 ? (message = 'You can drive.') : (message = 'You cannot drive.');

console.log(message);
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

#### Using the JavaScript ternary operator to perform multiple statements

```js
let authenticated = true;
let nextURL = authenticated
  ? (alert('You will redirect to admin area'), '/admin')
  : (alert('Access denied'), '/403');

// redirect to nextURL here
console.log(nextURL); // '/admin'
```

In this example, the returned value of the ternary operator is the last value in the comma-separated list.

#### Using multiple JavaScript ternary operators example

The following example shows how to use two ternary operators in the same expression:

```js
let speed = 90;
let message = speed >= 120 ? 'Too Fast' : speed >= 80 ? 'Fast' : 'OK';

console.log(message); // Fast
```

It’s a good practice to use the ternary operator when it makes the code easier to read. If the logic contains many `if...else` statements, you should avoid using the ternary operators.

