# JavaScript Primitive Wrapper Types

## Introduction to primitive wrapper types

JavaScript 提供了三种原始包装类型：Boolean、Number 和 String 类型。

原始包装类型使使用原始值（包括布尔值、数字和字符串）变得更加容易。

```js
let language = 'JavaScript';
let s = language.substring(4);
console.log(s);  // Script
```

在此示例中，变量 language 保存原始字符串值。它没有像 substring() 这样的方法。然而，上面的代码可以完美运行。

当对包含数字、字符串或布尔值的变量调用方法时，JavaScript 在幕后执行以下步骤：

- Create an object of a corresponding type.
- Call a specific method on the instance.
- Delete the instance immediately.

```js
let language = 'JavaScript';
let str = language.substring(4);
```

从技术上讲，等价于以下代码：

```js
let language = 'JavaScript';
// behind the scenes of the language.substring(4);
let tmp = new String(language);
str = temp.substring(4);
temp = null;
```

## Primitive wrapper types vs. reference types

当使用 new 运算符创建引用类型的对象时，该对象将保留在内存中，直到超出作用域。

以下变量 s 将保留在堆上，直到超出当前的变量作用域：

```js
let s = new String('JavaScript');
console.log(s);
```

然而，自动创建的原始包装器对象仅存在于一行代码中。

**严格模式下无法为基本数据类型添加属性，尝试为变量 s 添加属性会导致 TypeError: Cannot create property 'language' on string 'JavaScript'。**

```js
let s = 'JavaScript';
s.language = 'ECMAScript';
console.log(s.language); // undefined
```

尝试访问 s 变量的 language 属性，会收到一个 undefined 值，而不是“ECMAScript”。

原因是以下代码创建了一个 String 对象并为 language 属性赋值。

```js
s.language = 'ECMAScript';
```

然而，具有 language 属性的 String 对象仅在这行代码执行期间存在。