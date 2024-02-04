# JavaScript Optional Chaining Operator

## Introduction to the JavaScript optional chaining operator

可选的链接运算符 (?.) 就像访问一系列对象中的嵌套属性的快捷方式。可以使用运算符 ?，而不必检查链中的每个步骤是否为空（null 或 undefined）。直接访问所需的属性。

如果链的任何部分为空，则可选链接运算符 (?.) 将在那里停止并给出未定义的结果，无需为链中的每个步骤编写额外的检查。

假设有一个返回 user 对象的函数：

```js
function getUser(id) {
    if(id <= 0) {
        return null;
    }

    // get the user from database
    // and return null if id does not exist
    // ...
    
    // if user was found, return the user
    return {
        id: id,
        username: 'admin',
        profile: {
            avatar: '/avatar.png',
            language: 'English'
        }
    }
}
```

以下使用 getUser() 函数来访问 user profile：

```js
let user = getUser(1);
let profile = user.profile;
```

但是，如果传递的 id 小于或等于 0，或者数据库中不存在该 id，则 getUser() 函数将返回 null。

因此，在访问 avatar 属性之前，需要使用逻辑运算符 AND 检查用户是否不为 null：

```js
let user = getUser(2);
let profile = user && user.profile;
```

在此示例中，我们在访问 user.profile 属性的值之前确认用户不为 null 或 undefined。它可以防止如果直接访问 user.profile 而不先检查 user 而发生的错误。

ES2020 引入了可选链运算符，用问号后跟一个点表示：

```js
?.
```

要使用可选链接运算符访问对象的属性，可以使用以下方法之一：

```js
objectName ?. propertyName
objectName ?. [expression]
```

The optional chaining operator implicitly checks if the `user` is not `null` or `undefined` before attempting to access the `user.profile`:

```js
let user = getUser(2);
let profile = user ?. profile;
```

In this example, if the `user` is `null` or `undefined`, the optional chaining operator (`?.`) immediately returns `undefined`.

从技术上讲，它相当于如下：

```js
let user = getUser(2);
let profile = (user !== null && user !== undefined)
            ? user.profile
            : undefined;
```

### Stacking the optional chaining operator

如果 getUser() 返回的 user 对象没有 profile 属性。在不首先检查 user.profile 的情况下尝试访问 avatar 将导致错误。

为了避免错误，可以多次使用可选链接运算符，如下所示：

```js
let user = getUser(-1);
let avatar = user ?. profile ?. avatar;
```

在这种情况下，avatar 是 undefined。

### Combining with the nullish coalescing operator

If you want to assign a default profile to the `user`, you can combine the optional chaining operator (`?.`) with the nullish coalescing operator (`??`) as follows:

```js
let defaultProfile =  { default: '/default.png', language: 'English'};

let user = getUser(2);
let profile = user ?. profile ?? defaultProfile;
```

In this example, if the `user.profile` is `null` or `undefined`, the profile will take the `defaultProfile` due to the nullish coalescing operator.

## Using optional chaining operator with function calls

Suppose that you have a file API as follows:

```js
let file = {
    read() {
        return 'file content';
    },
    write(content) {
        console.log(`Writing ${content} to file...`);
        return true;
    }
};
```

This example calls the `read()` method of the `file` object:

```js
let data = file.read();
console.log(data);
```

If you call a method that doesn’t exist in the file object, you’ll get a TypeError:

```js
let compressedData = file.compress();
Uncaught TypeError: file.compress is not a function
```

However, if you use the optional chaining operator with the method call, the expression will return `undefined` instead of throwing an error:

```js
let compressedData = file.compress?.();
```

The `compressedData` is now `undefined`.

This is useful when you use an API in which a method might be not available for some reason e.g., a specific browser or device.

The following illustrates the syntax for using the optional chaining operator with a function or method call:

```js
functionName ?. (args)
```

The optional chaining operator (?.) is also helpful if you have a function with an optional callback:

```js
function getUser(id, callback) {
    // get user
    // ...

    let user = {
        id: id,
        username: 'admin'
    };

    // test if the callback exists
    if ( callback ) {
        callback(user);
    }

    return user;
}
```

By using the optional chaining operator, you can skip the test if the callback exists:

```js
function getUser(id, callback) {
    // get user
    // ...

    let user = {
        id: id,
        username: 'admin'
    };

    // test if the callback exists
    callback ?. (user);


    return user;
}
```