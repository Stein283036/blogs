# Objects

## Introduction to the JavaScript objects

在 JavaScript 中，对象是键值对的无序集合。每个键值对称为属性。

对象的 key 可以是任何字符串或者 symbol，其他类型会被自动地转换为字符串。

例如，当数字 `0` 被用作对象的属性的键时，会被转换为字符串 `"0"`：

```js
let obj = {
  0: "test" // 等同于 "0": "test"
};

// 都会输出相同的属性（数字 0 被转为字符串 "0"）
alert( obj["0"] ); // test
alert( obj[0] ); // test (相同的属性)
```

JavaScript 提供了多种创建对象的方法。最常用的一种是使用对象字面量表示法。

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

列表中的最后一个属性应以逗号结尾：

```js
let user = {
  name: "John",
  age: 30,
}
```

这叫做尾随（trailing）或悬挂（hanging）逗号。这样便于我们添加、删除和移动属性，因为所有的行都是相似的。

## Accessing properties

要访问对象的属性，可以使用两种表示法之一：dot notation 和 array-like notation。

当属性名称包含空格时，需要将其放在引号内。

dot notation 要求 `key` 是有效的变量标识符。这意味着：不包含空格，不以数字开头，也不包含特殊字符（允许使用 `$` 和 `_`）。

```js
let address = {
    'building no': 3960,
    street: 'North 1st street',
    state: 'CA',
    country: 'USA'
};
```

要访问 “building no” 属性，需要使用 array-like notation：

```js
address['building no'];
```

> 请注意，在对象的属性名称中使用空格不是一个好习惯。

方括号同样提供了一种可以通过任意表达式来获取属性名的方式 —— 与文本字符串不同 —— 例如下面的变量：

```js
let key = "likes birds";

// 跟 user["likes birds"] = true; 一样
user[key] = true;
```

在这里，变量 `key` 可以是程序运行时计算得到的，也可以是根据用户的输入得到的。然后我们可以用它来访问属性。这给了我们很大的灵活性。

当创建一个对象时，我们可以在对象字面量中使用方括号。这叫做 **计算属性**。

```js
let fruit = prompt("Which fruit to buy?", "apple");

let bag = {
  [fruit]: 5, // 属性名是从 fruit 变量中得到的
};

alert( bag.apple ); // 5 如果 fruit="apple"
```

计算属性的含义很简单：`[fruit]` 含义是属性名应该从 `fruit` 变量中获取。

可以在方括号中使用更复杂的表达式：

```js
let fruit = 'apple';
let bag = {
  [fruit + 'Computers']: 5 // bag.appleComputers = 5
};
```

方括号比点符号更强大。它允许任何属性名和变量，但写起来也更加麻烦。

所以，大部分时间里，当属性名是已知且简单的时候，就使用点符号。如果我们需要一些更复杂的内容，那么就用方括号。

读取不存在的属性将导致 `undefined`。例如：

```js
console.log(address.district); // undefined
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

JavaScript 的对象有一个需要注意的特性：能够被访问任何属性。即使属性不存在也不会报错！

读取不存在的属性只会得到 `undefined`。

```js
let user = {};
alert( user.noSuchProperty === undefined ); // true 意思是没有这个属性
```

为何会有 `in` 运算符呢？与 `undefined` 进行比较来判断还不够吗？

确实，大部分情况下与 `undefined` 进行比较来判断就可以了。但有一个例外情况，这种比对方式会有问题，但 `in` 运算符的判断结果仍是对的。

那就是属性存在，但存储的值是 `undefined` 的时候：

```js
let obj = {
  test: undefined
};
alert( obj.test ); // 显示 undefined，所以属性不存在？
alert( "test" in obj ); // true，属性存在！
```

这种情况很少发生，因为通常情况下不应该给对象赋值 `undefined`。我们通常会用 `null` 来表示未知的或者空的值。
