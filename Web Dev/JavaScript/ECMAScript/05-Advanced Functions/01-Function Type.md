# JavaScript Function Type

## Introduction to the JavaScript Function type

**在 JavaScript 中，所有函数都是对象。**它们是 Function 类型的实例。因为函数是对象，所以它们像其他对象一样具有属性和方法。

### Functions properties

每个函数都有几个（还有其它属性）重要的属性：length、name、prototype。

- length 属性确定函数声明中指定的命名参数的数量。
- prototype 属性引用实际的函数对象。
- name 属性指明函数的名称

```js
function add(x, y) {
    return x + y;
}

console.log(add.length); // 2
console.log(add.prototype);
```

add() 函数接受两个参数 x 和 y。因此，length 属性返回 2。

### new.target

通常像这样调用函数：

```js
let result = add(10,20);
console.log(result); // 30
```

另外，可以使用 new 关键字作为构造函数来调用函数：

```js
let obj = new add(10,20);
```

ES6 引入了 new.target 伪属性，检测是否使用 new 运算符调用了函数或构造函数。

如果函数被正常调用，则 new.target 是 undefined。但是，如果使用 new 关键字作为构造函数调用该函数，则 new.target 返回对构造函数的引用。

```js
function add(x, y) {
  console.log(new.target);
  return x + y;
}

let result = add(10, 20);
let obj = new add(10, 20);
undefined
[Function: add]
```

通过使用 new.target，可以控制函数的调用方式。

## Function methods: apply, call, and bind

函数对象具有三个重要的方法：apply()、call() 和 bind()。

### The `apply()` and `call()` methods

apply() 和 call() 方法使用给定的 this 值和参数调用函数。

apply() 和 call() 之间的区别在于，需要将参数作为类似数组的对象传递给 apply() 方法，而需要将参数单独传递给 call() 函数。

```js
let cat = { type: 'Cat', sound: 'Meow' };
let dog = { type: 'Dog', sound: 'Woof' };

const say = function (message) {
  console.log(message);
  console.log(this.type + ' says ' + this.sound);
};

say.apply(cat, ['What does a cat say?']);
say.apply(dog, ['What does a dog say?']);

What does a cat sound?
Cat says Meow
What does a dog sound?
Dog says Woof
```

call() 方法与 apply() 方法类似，只是将参数传递给函数的方式不同：

```js
say.call(cat, 'What does a cat say?');
say.call(dog, 'What does a dog say?');
```

### The `bind()` method

bind() 方法创建一个新的函数实例，其 this 值绑定到提供的对象。

首先，定义一个名为 car 的对象：

```js
let car = {
    speed: 5,
    start: function() {
        console.log('Start with ' + this.speed + ' km/h');
    }
};
```

然后，定义另一个名为 aircraft 的对象：

```js
let aircraft = {
    speed: 10,
    fly: function() {
        console.log('Flying');
    }
};
```

aircraft 没有 start() 方法。要启动 aircraft，可以使用 car 对象的 start() 方法的 bind() 方法：

```js
let taxiing = car.start.bind(aircraft);
```

In this statement, we change the `this` value inside the `start()` method of the `car` object to the `aircraft` object. The `bind()` method returns a new function that is assigned to the `taxiing` variable.

现在，可以通过 taxiing 变量调用 start() 方法：

```js
taxiing();
Start with 10 km/h
```

从技术上讲，aircraft 对象通过 bind()、call() 或 apply() 方法借用了 car 对象的 start() 方法。

因此，bind()、call() 和 apply() 方法也称为借用函数（borrowing functions）。