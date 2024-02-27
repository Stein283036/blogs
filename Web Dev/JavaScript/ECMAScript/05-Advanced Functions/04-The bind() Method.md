# JavaScript bind() Method

## Introduction to JavaScript `bind()` method

bind() 方法返回一个新函数，调用时将其 this 设置为特定值。

```js
fn.bind(thisArg[, arg1[, arg2[, ...]]])
```

在此语法中，bind() 方法返回函数 fn 的副本，其中包含特定的 this 值 (thisArg) 和参数 (arg1、arg2、...)。

与 call() 和 apply() 方法不同，bind() 方法**不会立即执行该函数**。它只是返回函数的新版本，该函数的 this 设置为 thisArg 参数。

## Using JavaScript `bind()` for function binding

```js
let person = {
    name: 'John Doe',
    getName: function() {
        console.log(this.name);
    }
};

setTimeout(person.getName, 1000); // undefined
```

从输出中可以清楚地看到，person.getName() 返回 undefined 而不是“John Doe”。

这是因为 setTimeout() 接收的函数 person.getName 与 person 对象是分开的。

该声明：

```js
setTimeout(person.getName, 1000);
```

可以重写为：

```js
let f = person.getName;
setTimeout(f, 1000); // // lost person context
```

setTimeout() 函数中的 this 在非严格模式下设置为全局对象，在严格模式下是 undefined。

因此，当调用回调 person.getName 时，全局对象中不存在该名称，它被设置为 undefined。

要解决此问题，可以将对 person.getName 方法的调用包装在匿名函数中，如下所示：

```js
setTimeout(function () {
    person.getName();
}, 1000);
```

这是有效的，因为它从外部范围获取 person，然后调用方法 getName()。

或者可以使用 bind() 方法：

```js
let f = person.getName.bind(person);
setTimeout(f, 1000);
```

## Using `bind()` to borrow methods from a different object

假设有一个具有 run() 方法的 runner 对象：

```js
let runner = {
    name: 'Runner',
    run: function(speed) {
        console.log(this.name + ' runs at ' + speed + ' mph.');
    }
};
```

以及具有 fly() 方法的 flyer 对象：

```js
let flyer = {
    name: 'Flyer',
    fly: function(speed) {
        console.log(this.name + ' flies at ' + speed + ' mph.');
    }
};
```

如果希望 fly 对象能够调用 run 方法，可以使用 bind() 方法创建 run() 函数，并将 this 设置为 fly 对象：

```js
let flyRun = runner.run.bind(flyer, 20);
flyRun(); // Flyer runs at 20 mph.
```

在 JavaScript 中，借用对象的方法而不复制该方法并在两个不同的位置维护它的能力非常强大。