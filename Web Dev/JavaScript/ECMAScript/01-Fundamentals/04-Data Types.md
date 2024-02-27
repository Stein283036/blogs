# Data Types

Primitive data types:

- null
- undefined
- boolean
- number
- string
- symbol – available from ES2015
- bigint – available from ES2020

Complex data type:

- object

## typeof

`typeof` 运算符用来确定变量存储的值的类型。

有两个例外：

```javascript
typeof null == "object" // JavaScript 编程语言的设计错误
typeof function(){} == "function" // 函数被特殊对待
```

## The undefined type

The `undefined` type is a primitive type that has only one value `undefined`. By default, when a variable is declared but not initialized, it defaults to `undefined`.

```js
let counter;
console.log(counter);        // undefined
console.log(typeof counter); // undefined
```

## The null type

null 类型是一种基本数据类型，也只有一个值 null。

```js
let obj = null;
console.log(typeof obj); // object
```

typeof null 返回 object 是 JavaScript 中的一个已知错误。由于可能破坏许多现有站点，修复提案被拒绝。

JavaScript 定义 null 等于 undefined：

```js
console.log(null == undefined); // true
```

## The number type

JavaScript 使用 number 类型来表示整数和浮点数。

number 类型有三个特殊值：Infinity、-Infinity、NaN。

请注意，如果浮点数看起来是整数，JavaScript 会自动将浮点数转换为整数。

原因是 Javascript 总是希望使用更少的内存，因为浮点值使用的内存是整数值的两倍。

```js
let price = 200.00; // interpreted as an integer 200
```

要获取 number 类型的范围，请使用 Number.MIN_VALUE 和 Number.MAX_VALUE。

```js
console.log(Number.MAX_VALUE); // 1.7976931348623157e+308
console.log(Number.MIN_VALUE); // 5e-324
```

可以使用 Infinity 和 -Infinity 来表示无限数：

```js
console.log(Number.MAX_VALUE + Number.MAX_VALUE); // Infinity
console.log(-Number.MAX_VALUE - Number.MAX_VALUE); // -Infinity
```

### NaN

NaN 代表非数字。它是一个特殊的数值，表示无效数字。例如，字符串除以数字会返回 NaN：

```js
console.log('a'/2); // NaN;
```

NaN 有两个特殊的特性： 

- 任何与 NaN 的运算都会返回 NaN。 
- NaN 不等于任何值，包括其本身。

```js
console.log(NaN/2); // NaN
console.log(NaN == NaN); // false
```

## The string type

在 JavaScript 中，字符串是零个或多个字符的序列。

如果要在文字字符串中使用单引号或双引号，则需要使用反斜杠对其进行转义。

```js
let message = 'I\'m also a valid string'; // use \ to escape the single quote (')
```

JavaScript 字符串是不可变的，这意味着它们一旦创建就无法修改。可以从现有字符串创建新字符串。例如：

```js
let str = 'JavaScript';
str = str + ' String';
```

在幕后，JavaScript 引擎创建一个新字符串，其中包含新字符串“JavaScript String”，并销毁原始字符串“JavaScript”和“String”。

ES6 引入了 literal template，允许定义字符串反引号 (`) 字符：

```js
let name = `John`';
```

模板字符串允许在字符串内使用单引号和双引号，而无需转义它们。

```js
let mesage = `"I'm good". She said";
```

此外，可以将变量和表达式放置在模板字符串中。 JavaScript 会将变量替换为字符串中的值。这称为字符串插值。

```js
let name = 'John';
let message = `Hi, I'm ${name}.`;

console.log(message);
```

`length` 属性返回字符串的长度：

```js
let str = "Good Morning!";
console.log(str.length);  // 13
```

请注意，JavaScript 具有 String 类型（字母 S 大写），它是原始字符串类型的原始包装类型。因此，可以从原始字符串访问 String 类型的所有属性和方法。

要**访问**字符串中的字符，可以使用类似数组的 [] 表示法和从零开始的索引。

```js
let str = "Hello";
console.log(str[0]); // "H"
```

要**连接**两个或多个字符串，可以使用 + 运算符：

```js
let name = 'John';
let str = 'Hello ' + name;

console.log(str); // "Hello John"
```

要将非字符串值**转换**为字符串，使用以下方法之一：

- String(n);
- ” + n
- n.toString()

注意，toString() 方法不适用于 undefined 和 null。

在JavaScript中，字符串**比较**可以使用比较运算符（如 `<`, `>`, `<=`, `>=`, `==`）或字符串的比较方法（`localeCompare()`方法）来实现。

字符串的比较是基于字典顺序的。JavaScript使用Unicode字符顺序来比较字符串，所以实际比较的是字符的**Unicode码点**。

`localeCompare()` 方法可以更好地处理一些语言特有的排序规则，因为它可以根据本地语言环境来进行比较。

## The boolean type

布尔类型有两个字面值：小写的 true 和 false。

```js
let inProgress = true;
let completed = false;

console.log(typeof completed); // boolean
```

JavaScript 允许将其他类型的值转换为 true 或 false 的布尔值。

要将其他类型的值转换为布尔值，使用 Boolean() 函数。

转换规则：

| Type      | true                         | false        |
| :-------- | :--------------------------- | :----------- |
| string    | non-empty string             | empty string |
| number    | non-zero number and Infinity | 0, 0.0, NaN  |
| object    | non-null object              | null         |
| undefined |                              | undefined    |

该表很重要，因为某些语句使用 Boolean() 函数自动将非布尔值转换为布尔值。

例如，if 语句在条件为 true 时执行块。如果您使用非布尔值，它将使用 Boolean() 函数将该值隐式转换为布尔值。

```js
let error = 'An error occurred';

if (error) {
  console.log(error);
}
An error occurred
```

## The symbol type

JavaScript 在 ES6 中引入了一种新的原始类型：symbol。与其他基本类型不同，符号类型没有字面形式。

要创建符号，调用 Symbol 函数：

```js
let s1 = Symbol();
```

每次调用 Symbol 函数时都会创建一个新的唯一值。

```js
console.log(Symbol() == Symbol()); // false
```

## The bigint type

bigint 类型表示大于 2^53^ – 1 或小于 -(2^53^ – 1) 的整数。

```js
let pageView = 9007199254740991n;
console.log(typeof(pageView)); // 'bigint'
```

## The object type

在 JavaScript 中，对象是属性的集合，其中每个属性都定义为键值对，键必须是 string 或者 symbol 类型，值可以是其它合法的数据类型。

对象的属性名称可以是任何字符串。如果属性名称不是有效标识符，则可以在属性名称周围使用引号。

例如，如果 person 对象具有属性 first-name，则必须将其放在引号中，例如 “first-name”。

对象字面量语法创建对象：

```js
let obj = {}
let obj = {
    name: 'stein',
    age: 23
}
```

```js
let contact = {
    firstName: 'John',
    lastName: 'Doe',
    email: 'john.doe@example.com',
    phone: '(408)-555-9999',
    address: {
        building: '4000',
        street: 'North 1st street',
        city: 'San Jose',
        state: 'CA',
        country: 'USA'
    }
}
```

要访问对象的属性，可以使用：

- The dot notation (`.`)
- The array-like notation (`[]`).

```js
console.log(contact.firstName);
console.log(contact.lastName);
```

```javascript
console.log(contact['phone']); // '(408)-555-9999'
console.log(contact['email']); // 'john.doe@example.com'
```

如果引用不存在的属性，将得到一个未定义的值。

```js
console.log(contact.age); // undefined
```
