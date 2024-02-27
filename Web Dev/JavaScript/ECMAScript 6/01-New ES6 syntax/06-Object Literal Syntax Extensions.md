# Object Literal Syntax Extensions in ES6

由于其简单性，对象字面量是在 JavaScript 中创建对象的最流行的模式之一。 ES6 通过在某些方面扩展语法，使对象字面量更加简洁和强大。

## Object property initializer shorthand

在 ES6 之前，对象字面量是名称-值对的集合。

```js
function createMachine(name, status) {
    return {
        name: name,
        status: status
    };
}
```

name 和 status 属性采用 name 和 status 形参的值。此语法看起来多余，因为 name 和 status 在属性的 name 和 value 中都提到了两次。

当对象的属性与局部变量名称相同时，ES6 允许通过包含不带冒号和值的名称来消除重复。

例如，可以在 ES6 中重写 createMachine() 函数，如下所示：

```js
function createMachine(name, status) {
    return {
        name,
        status
    };
}
```

在内部，当对象字面量的属性只有名称时，JavaScript 引擎会在周围范围内搜索具有相同名称的变量。如果 JavaScript 引擎可以找到一个，它就会将该变量的值分配给该属性。

同样，可以从局部变量构造对象字面量，如下例所示：

```js
let name = 'Computer',
    status = 'On';
let machine = {
    name,
    status
}
```

## Computed property name

在 ES6 之前，可以使用方括号 ([]) 为对象的属性启用计算属性名称。

方括号 [] 允许使用字符串文字和变量作为属性名称。

```js
let name = 'machine name';
let machine = {
    [name]: 'server',
    'machine hours': 10000
};

console.log(machine[name]); // server
console.log(machine['machine hours']); // 10000
```

在 ES6 中，计算属性名称是对象字面量语法的一部分，并且使用方括号表示法。

当属性名称放在方括号内时，JavaScript 引擎将其作为字符串进行计算。这意味着可以使用表达式作为属性名称。

```js
let prefix = 'machine';
let machine = {
    [prefix + ' name']: 'server',
    [prefix + ' hours']: 10000
};

console.log(machine['machine name']); // server
console.log(machine['machine hours']); // 10000
```

The `machine` object’s properties evaluated to `'machine name'` and `'machine hours'`, therefore you can reference them as the properties of the `machine` object.

## Concise method syntax

在 ES6 之前，为对象字面量定义方法时，需要指定名称和完整函数定义：

```js
let server = {
	name: "Server",
	restart: function () {
		console.log("The" + this.name + " is restarting...");
	}
};
```

ES6 通过删除冒号 (:) 和 function 关键字，使对象字面量方法的语法更加简洁。

```js
let server = {
	name: "Server",
	restart() {
		console.log("The" + this.name + " is restarting...");
	}
};
```

这种简写语法也称为简洁方法语法。属性名称中包含空格是有效的。

```js
let server = {
    name: 'Server',
    restart() {
        console.log("The " + this.name + " is restarting...");
    },
    'starting up'() {
        console.log("The " +  this.name + " is starting up!");
    }
};

server['starting up']();
```