# JavaScript Boolean

## JavaScript boolean primitive type

JavaScript 提供了一个布尔原始类型，它有 true 和 false 两个值。

```js
let isPending = false;
let isDone = true;
```

将 typeof 运算符应用于保存原始布尔值的变量时，返回 boolean。

```js
console.log(typeof(isPending)); //  boolean
console.log(typeof(isDone)); // boolean
```

## JavaScript Boolean object

除了 boolean 原始类型之外，JavaScript 还提供了全局 Boolean() 函数，用于将其他类型的值转换为布尔值。

```js
let a = Boolean(' ');
console.log(a); // true
console.log(typeof(a)); // boolean
```

Boolean 也是布尔原始类型的包装对象。这意味着将 true 或 false 传递给 Boolean 构造函数时，它将创建一个 Boolean 对象。

```js
let b = new Boolean(false);
```

要取回原始值，调用 Boolean 对象的 valueOf() 方法：

```js
console.log(b.valueOf()); // false
```

但是，如果调用 Boolean 对象的 toString() 方法，将获得字符串值“true”或“false”。

```js
console.log(b.toString()); // "false"
```

## JavaScript boolean vs. Boolean

```js
let completed = true;
let active = new Boolean(false);
```

首先，active 是一个对象，因此可以向其添加属性：

```js
active.primitiveValue = active.valueOf();
console.log(active.primitiveValue); // false
```

但是，不能使用原始布尔变量（例如 completed 变量）来执行此操作：

```js
completed.name = 'primitive';
console.log(completed.name); // undefined
```

其次，Boolean 对象的 typeof 返回 object，而原始布尔值的 typeof 返回 boolean。

```js
console.log(typeof completed); // boolean
console.log(typeof active); // object
```

最好不要使用布尔对象，因为它会造成很多混乱，尤其是在表达式中使用时。

```js
let falseObj = new Boolean(false);
if (falseObj) {
    console.log('weird part of the Boolean object');
}
```

使用 Boolean() 函数将不同类型的值转换为 boolean 值，但切勿将 Boolean 用作原始布尔值的包装对象。
