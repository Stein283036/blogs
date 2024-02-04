# JavaScript const: Declaring Constants in ES6

## Introduction to the JavaScript const keyword

ES6 提供了一种使用 const 关键字声明常量的新方法。 const 关键字创建对值的只读引用。

```js
const CONSTANT_NAME = value;
```

按照惯例，常量标识符的单词是全大写的，单词之间使用 _ 分隔。

与 let 关键字一样，const 关键字声明 block-scoped 变量。然而，const关键字声明的块作用域变量不能被重新赋值。

与 let 关键字不同的是需要将值初始化为 const 关键字声明的变量。

由于 const 变量声明中缺少初始值设定项而导致 SyntaxError：

```js
const RED;
SyntaxError: Missing initializer in const declaration
```

## JavaScript const and Objects

const 关键字确保它创建的变量是只读的。但是，这并不意味着 const 变量引用的实际值是不可变的。

```js
const person = { age: 20 };
person.age = 30; // OK
console.log(person.age); // 30
```

但是，不能像这样为 person 常量重新分配不同的值：

```js
person = { age: 40 }; // TypeError
```

如果希望 person 对象的值不可变，则必须使用 Object.freeze() 方法冻结它：

```js
const person = Object.freeze({age: 20});
person.age = 30; // TypeError
```

注意，Object.freeze() 是浅层的，这意味着它可以冻结对象的属性，而不是属性引用的对象。

For example, the `company` object is constant and frozen.

```js
const company = Object.freeze({
    name: 'ABC corp',
    address: {
        street: 'North 1st street',
        city: 'San Jose',
        state: 'CA',
        zipcode: 95134
    }
});
```

但 company.address 引用的对象值不是不可变的，可以向 company.address 对象添加一个新属性，如下所示：

```js
company.address.country = 'USA'; // OK
```

## JavaScript const and Arrays

```js
const colors = ['red'];
colors.push('green');
console.log(colors); // ["red", "green"]

colors.pop();
colors.pop();
console.log(colors); // []

colors = []; // TypeError
```

## JavaScript `const` in a `for` loop

ES6 提供了一个名为 for...of 的新构造，它允许创建一个迭代可迭代对象（例如数组、字符串、映射和集合）的循环。

```js
let scores = [75, 80, 95];

for (let score of scores) {
	console.log(score);
}
```

如果不打算修改循环内的score变量，你可以使用const关键字来代替：

```js
let scores = [75, 80, 95];
for (const score of scores) {
    console.log(score);
}
```

for...of 在每次循环迭代中为 const 关键字创建一个新绑定。换句话说，每次迭代都会创建一个新的分数常量。