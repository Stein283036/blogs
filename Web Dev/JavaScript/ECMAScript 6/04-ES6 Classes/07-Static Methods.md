# JavaScript Static Methods

## Introduction to the JavaScript static methods

根据定义，静态方法绑定到类，而不是该类的实例。因此，静态方法对于定义帮助或工具方法很有用。

在 ES6 之前定义静态方法，可以直接将其添加到类的构造函数中。例如，假设有一个 Person 类型，如下所示：

```js
function Person(name) {
    this.name = name;
}

Person.prototype.getName = function () {
    return this.name;
};
```

下面向 Person 类型添加一个名为 createAnonymous() 的静态方法：

```js
Person.createAnonymous = function (gender) {
    let name = gender == "male" ? "John Doe" : "Jane Doe";
    return new Person(name);
};
```

createAnonymous() 方法被视为静态方法，因为它的属性值不依赖于 Person 类型的任何实例。

要调用 createAnonymous() 方法，请使用 Person 类型而不是其实例：

```js
var anonymous = Person.createAnonymous();
```

## JavaScript static methods in ES6

在 ES6 中，可以使用 static 关键字定义静态方法。以下示例为 Person 类定义了一个名为 createAnonymous() 的静态方法：

```js
class Person {
	constructor(name) {
		this.name = name;
	}
	getName() {
		return this.name;
	}
	static createAnonymous(gender) {
		let name = gender == "male" ? "John Doe" : "Jane Doe";
		return new Person(name);
	}
}
```

要调用静态方法，请使用以下语法：

```js
let anonymous = Person.createAnonymous("male");
```

不能从类的实例调用静态方法，将收到错误。

```js
let person = new Person('James Doe');
let anonymous = person.createAnonymous("male");
TypeError: person.createAnonymous is not a function
```