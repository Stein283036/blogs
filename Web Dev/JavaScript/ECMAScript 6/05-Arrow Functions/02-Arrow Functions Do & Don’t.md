# When You Should Not Use Arrow Functions

箭头函数没有自己的 this 值和参数对象。因此，不应该将其用作事件处理程序、对象字面量的方法、原型方法，或者使用 arguments 对象的函数。

## Event handlers

假设有以下输入文本字段：

```html
<input type="text" name="username" id="username" placeholder="Enter a username">
```

希望在用户输入用户名时显示一条问候消息。下面显示了将显示问候消息的 <div> 元素：

```html
<div id="greeting"></div>
```

用户输入用户名后，捕获输入的当前值并将其更新到 <div> 元素：

```js
const greeting = document.querySelector('#greeting');
const username = document.querySelector('#username');
username.addEventListener('keyup', () => {
  greeting.textContent = 'Hello ' + this.value;
});
```

但是，当执行代码时，无论您输入什么内容，都会收到以下消息：

```js
Hello undefined
```

这意味着事件处理程序中的 this.value 始终返回 undefined。

如前所述，箭头函数没有自己的 this 值。它使用封闭词法范围的 this 值。在上面的示例中，箭头函数中的 this 引用了全局对象。

在网络浏览器中，全局对象是 window。 window 对象没有 value 属性。因此，JavaScript 引擎将 value 属性添加到 window 对象并将其值设置为 undefined。

要解决此问题，需要使用常规函数。 this 值将绑定到触发事件的 <input> 元素。

```js
username.addEventListener('keyup', function () {
    input.textContent = 'Hello ' + this.value;
});
```

## Object methods

以下是一个 counter 对象：

```js
const counter = {
  count: 0,
  next: () => ++this.count,
  current: () => this.count
};
```

counter 对象有两个方法：current() 和 next()。 current() 方法返回当前计数器值，next() 方法返回下一个计数器值。

下面显示了下一个计数器值，该值应为 1：

```js
console.log(counter.next());
```

但是，它返回 NaN。

原因是，当在对象内部使用箭头函数时，它会从封闭的词法范围（本例中为全局范围）继承 this 值。

next() 方法中的 this.count 相当于 window.count（在 Web 浏览器中）。

window.count 默认是 undefined，因为window对象没有count属性。 next() 方法将 undefined 加一，结果为 NaN。

要解决此问题，可以使用常规函数作为对象字面量的方法，如下所示：

```js
const counter = {
    count: 0,
    next() {
        return ++this.count;
    },
    current() {
        return this.count;
    }
};
```

## Prototype methods

以下使用原型模式的 Counter 对象：

```js
function Counter() {
    this.count = 0;
}

Counter.prototype.next = () => {
    return this.count;
};

Counter.prototype.current = () => {
    return ++this.next;
}
```

next() 和 current() 方法中的 this 值引用全局对象。由于希望方法中的 this 值引用 Counter 对象，因此需要使用常规函数：

```js
function Counter() {
    this.count = 0;
}

Counter.prototype.next = function () {
    return this.count;
};

Counter.prototype.current = function () {
    return ++this.next;
}
```

## Functions that use the arguments object

箭头函数没有 arguments 对象。因此，如果有一个使用 arguments 对象的函数，则不能使用箭头函数。

例如，以下 concat() 函数将不起作用：

```js
const concat = (separator) => {
    let args = Array.prototype.slice.call(arguments, 1);
    return args.join(separator);
}
```

相反，可以使用如下常规函数：

```js
function concat(separator) {
    let args = Array.prototype.slice.call(arguments, 1);
    return args.join(separator);
}
```