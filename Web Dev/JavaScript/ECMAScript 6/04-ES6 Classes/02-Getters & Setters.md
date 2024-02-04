# JavaScript Getters and Setters

## Introduction to the JavaScript getters and setters

以下示例定义了一个名为 Person 的类：

```js
class Person {
    constructor(name) {
        this.name = name;
    }
}

let person = new Person("John");
console.log(person.name); // John
```

Person 类有一个属性名称和一个构造函数。构造函数将 name 属性初始化为字符串。

有时，不希望像这样直接访问 name 属性：

```js
person.name
```

为此，可以想出一对操作 name 属性的方法。例如：

```js
class Person {
    constructor(name) {
        this.setName(name);
    }
    getName() {
        return this.name;
    }
    setName(newName) {
        newName = newName.trim();
        if (newName === '') {
            throw Error('The name cannot be empty');
        }
        this.name = newName;
    }
}

let person = new Person('Jane Doe');
console.log(person); // Jane Doe

person.setName('Jane Smith');
console.log(person.getName()); // Jane Smith
```

getName() 和 setName() 方法在其他编程语言（例如 Java 和 C++）中称为 getter 和 setter。

ES6 提供了使用 get 和 set 关键字定义 getter 和 setter 的特定语法。例如：

```js
class Person {
    constructor(name) {
        this._name = name;
    }
    get name() {
        return this._name;
    }
    set name(newName) {
        newName = newName.trim();
        if (newName === '') {
            throw 'The name cannot be empty';
        }
        this._name = newName;
    }
}
```

首先，将 name 属性更改为 _name 以避免与 getter 和 setter 发生名称冲突。

其次，getter 使用 get 关键字，后跟方法名称：

```js
get name() {
    return this._name;
}
```

要调用 getter，可以使用以下语法：

```js
let name = person.name;
```

当 JavaScript 看到对 Person 类的 name 属性的访问时，它会检查 Person 类是否具有任何 name 属性。

如果没有，JavaScript 将检查 Person 类是否具有绑定到 name 属性的任何方法。在此示例中，name() 方法通过 get 关键字绑定到 name 属性。一旦 JavaScript 找到 getter 方法，它就会执行 getter 方法并返回一个值。

第三，setter 使用 set 关键字，后跟方法名称：

```js
set name(newName) {
    newName = newName.trim();
    if (newName === '') {
        throw 'The name cannot be empty';
    }
    this._name = newName;
}
```

当为 name 属性赋值时，JavaScript 将调用 name() setter，如下所示：

```js
person.name = 'Jane Smith';
```

如果一个类只有 getter 而没有 setter，并且尝试使用 setter，则更改不会生效。请参见以下示例：

```js
class Person {
    constructor(name) {
        this._name = name;
    }
    get name() {
        return this._name;
    }
}

let person = new Person("Jane Doe");
console.log(person.name);

// attempt to change the name, but cannot
person.name = 'Jane Smith';
console.log(person.name); // Jane Doe
```

## Using getter in an object literal

The following example defines a getter called `latest` to return the latest attendee of the `meeting` object:

```js
let meeting = {
    attendees: [],
    add(attendee) {
        console.log(`${attendee} joined the meeting.`);
        this.attendees.push(attendee);
        return this;
    },
    get latest() {
        let count = this.attendees.length;
        return count == 0 ? undefined : this.attendees[count - 1];
    }
};

meeting.add('John').add('Jane').add('Peter');
console.log(`The latest attendee is ${meeting.latest}.`);
```