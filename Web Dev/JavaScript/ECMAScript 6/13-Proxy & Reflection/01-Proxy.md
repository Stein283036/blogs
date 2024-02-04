# JavaScript Proxy

## What is a JavaScript Proxy object

A JavaScript Proxy is an object that wraps another object (target) and intercepts the fundamental operations of the target object.

The fundamental operations can be the property lookup, assignment, enumeration, function invocations, etc.

## Creating a proxy object

```js
let proxy = new Proxy(target, handler);
```

- `target` – is an object to wrap.
- `handler` – is an object that contains methods to control the behaviors of the `target`. The methods inside the `handler` object are called **traps**.

## A simple proxy example

First, define an object called `user`:

```js
const user = {
    firstName: 'John',
    lastName: 'Doe',
    email: 'john.doe@example.com',
}
```

Second, define a `handler` object:

```js
const handler = {
    get(target, property) {
        console.log(`Property ${property} has been read.`);
        return target[property];
    }
}
```

Third, create a `proxy` object:

```js
const proxyUser = new Proxy(user, handler);
```

The `proxyUser` object uses the `user` object to store data. The `proxyUser` can access all properties of the `user` object.

![JavaScript Proxy](D:\2024年\blogs\Web Dev\JavaScript\ECMAScript 6\13-Proxy & Reflection\assets\JavaScript-Proxy.png)

Fourth, access the `firstName` and `lastName` properties of the `user` object via the `proxyUser` object:

```js
console.log(proxyUser.firstName);
console.log(proxyUser.lastName);
```

输出：

```js
Property firstName has been read.
John
Property lastName has been read.
Doe
```

When you access a property of the `user` object via the `proxyUser` object, the `get()` method in the `handler` object is called.

Fifth, if you modify the original object `user`, the change is reflected in the `proxyUser`:

```js
user.firstName = 'Jane';
console.log(proxyUser.firstName);
```

输出：

```js
Property firstName has been read.
Jane
```

Similarly, a change in the `proxyUser` object will be reflected in the original object (`user`):

```js
proxyUser.lastName = 'William';
console.log(user.lastName); // William
```

## Proxy Traps

### The `get()` trap

The `get()` trap is fired when a property of the `target` object is accessed via the proxy object.

Generally, you can develop a custom logic in the `get()` trap when a property is accessed.

For example, you can use the `get()` trap to define **computed properties** for the target object. The computed properties are properties whose values are calculated based on values of existing properties.

The `user` object does not have a property `fullName`, you can use the `get()` trap to create the `fullName` property based on the `firstName` and `lastName` properties:

```js
const user = {
    firstName: 'John',
    lastName: 'Doe'
}
const handler = {
    get(target, property) {
        return property === 'fullName' ?
            `${target.firstName} ${target.lastName}` :
            target[property];
    }
};
const proxyUser = new Proxy(user, handler);
console.log(proxyUser.fullName); // John Doe
```

### The `set()` trap

The `set()` trap controls behavior when a property of the `target` object is set.

The `set()` trap controls behavior when a property of the `target` object is set.

Suppose that the `age` of the user must be greater than 18. To enforce this constraint, you develop a `set()` trap as follows:

```js
const user = {
    firstName: 'John',
    lastName: 'Doe',
    age: 20
}
const handler = {
    set(target, property, value) {
        if (property === 'age') {
            if (typeof value !== 'number') {
                throw new Error('Age must be a number.');
            }
            if (value < 18) {
                throw new Error('The user must be 18 or older.')
            }
        }
        target[property] = value;
    }
};
const proxyUser = new Proxy(user, handler);
```

First, set the `age` of user to a string:

```js
proxyUser.age = 'foo';
Error: Age must be a number.
```

Second, set the age of the user to 16:

```js
proxyUser.age = '16';
The user must be 18 or older.
```

Third, set the age of the user to 21:

```js
proxyUser.age = 21
```

## The `apply()` trap

The `handler.apply()` method is a trap for a function call.

```js
let proxy = new Proxy(target, {
    apply: function(target, thisArg, args) {
        //...
    }
});
```

See the following example:

```js
const user = {
    firstName: 'John',
    lastName: 'Doe'
}
const getFullName = function (user) {
    return `${user.firstName} ${user.lastName}`;
}
const getFullNameProxy = new Proxy(getFullName, {
    apply(target, thisArg, args) {
        return target(...args).toUpperCase();
    }
});
console.log(getFullNameProxy(user)); // JOHN DOE
```

## More traps

- `construct` – traps usage of the `new` operator
- `getPrototypeOf` – traps an internal call to `[[GetPrototypeOf]]`
- `setPrototypeOf` – traps a call to `Object.setPrototypeOf`
- `isExtensible` – traps a call to `Object.isExtensible`
- `preventExtensions` – traps a call to `Object.preventExtensions`
- `getOwnPropertyDescriptor` – traps a call to `Object.getOwnPropertyDescriptor`
