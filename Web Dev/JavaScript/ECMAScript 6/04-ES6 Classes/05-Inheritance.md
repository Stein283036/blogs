# JavaScript Inheritance Using extends & super

## Implementing JavaScript inheritance using `extends` and `super`

在 ES6 之前，实现正确的继承需要多个步骤。最常用的策略之一是原型继承。

下面说明了 Bird 如何使用原型继承技术从 Animal 继承属性：

```js
function Animal(legs) {
    this.legs = legs;
}

Animal.prototype.walk = function() {
    console.log('walking on ' + this.legs + ' legs');
}

function Bird(legs) {
    Animal.call(this, legs);
}

Bird.prototype = Object.create(Animal.prototype);
Bird.prototype.constructor = Bird;

Bird.prototype.fly = function() {
    console.log('flying');
}

var pigeon = new Bird(2);
pigeon.walk(); // walking on 2 legs
pigeon.fly();  // flying
```

ES6 通过使用 extends 和 super 关键字简化了这些步骤。

以下示例定义了 Animal 和 Bird 类，并通过 extends 和 super 关键字建立了继承。

```js
class Animal {
    constructor(legs) {
        this.legs = legs;
    }
    walk() {
        console.log('walking on ' + this.legs + ' legs');
    }
}

class Bird extends Animal {
    constructor(legs) {
        super(legs);
    }
    fly() {
        console.log('flying');
    }
}


let bird = new Bird(2);

bird.walk();
bird.fly();
```

首先，使用extends关键字使Bird类继承自Animal类：

```js
class Bird extends Animal {
   // ...
}
```

Animal 类称为基类或父类，而 Bird 类称为派生类或子类。通过这样做，Bird 类继承了 Animal 类的所有方法和属性。

其次，在 Bird 的构造函数中，调用 super() 以使用 legs 参数调用 Animal 的构造函数。

如果子类具有构造函数，则 JavaScript 要求子类调用 super()。正如在 Bird 类中看到的，super(legs) 相当于 ES5 中的以下语句：

```js
Animal.call(this, legs);
```

如果 Bird 类没有构造函数，则无需执行任何其他操作：

```js
class Bird extends Animal {
    fly() {
        console.log('flying');
    }
}
```

它相当于下面的类：

```js
class Bird extends Animal {
    constructor(...args) {
        super(...args);
    }
    fly() {
        console.log('flying');
    }
}
```

然而，子类有一个构造函数，它需要调用super()。例如，以下代码会导致错误：

```js
class Bird extends Animal {
    constructor(legs) {
    }
    fly() {
        console.log('flying');
    }
}
ReferenceError: Must call super constructor in derived class before accessing 'this' or returning from derived constructor
```

**因为super()初始化了this对象，所以在访问this对象之前需要调用super()。在调用 super() 之前尝试访问 this 也会导致错误。**

> this 引用的对象是在子类创建并且返回对象的引用，传递到父类构造器的是 this 引用。

例如，如果要初始化 Bird 类的 color 属性，可以按如下方式进行：

```js
class Bird extends Animal {
	constructor(legs, color) {
		super(legs);
		this.color = color;
	}
	fly() {
		console.log("flying");
	}
	getColor() {
		return this.color;
	}
}

let pegion = new Bird(2, "white");
console.log(pegion.getColor());
```

## Shadowing methods

ES6允许子类和父类有同名的方法。在这种情况下，当你调用子类的对象的方法时，子类中的方法将隐藏父类中的方法。

下面的 Dog 类扩展了 Animal 类并重新定义了 walk() 方法：

```js
class Dog extends Animal {
    constructor() {
        super(4);
    }
    walk() {
        console.log(`go walking`);
    }
}

let bingo = new Dog();
bingo.walk(); // go walking
```

要在子类中调用父类的方法，可以使用 super.method(arguments) ，如下所示：

```js
class Dog extends Animal {
    constructor() {
        super(4);
    }
    walk() {
        super.walk();
        console.log(`go walking`);
    }
}

let bingo = new Dog();
bingo.walk();
// walking on 4 legs
// go walking
```

## Inheriting static members

除了属性和方法之外，子类还继承父类的所有静态属性和方法。

```js
class Animal {
    constructor(legs) {
        this.legs = legs;
    }
    walk() {
        console.log('walking on ' + this.legs + ' legs');
    }
    static helloWorld() {
        console.log('Hello World');
    }
}

class Bird extends Animal {
    fly() {
        console.log('flying');
    }
}
```

在此示例中，Animal 类具有 helloWorld() 静态方法，该方法可用作 Bird.helloWorld()，其行为与 Animal.helloWorld() 方法相同：

```js
Bird.helloWorld(); // Hello World
```

## Inheriting from built-in types

JavaScript 允许通过继承来扩展内置类型，例如 Array、String、Map 和 Set。

以下 Queue 类扩展了 Array 引用类型。语法比使用构造函数/原型模式实现的队列干净得多。

```js
class Queue extends Array {
    enqueue(e) {
        super.push(e);
    }
    dequeue() {
        return super.shift();
    }
    peek() {
        return !this.empty() ? this[0] : undefined;
    }
    empty() {
        return this.length === 0;
    }
}

var customers = new Queue();
customers.enqueue('A');
customers.enqueue('B');
customers.enqueue('C');

while (!customers.empty()) {
    console.log(customers.dequeue());
}
```