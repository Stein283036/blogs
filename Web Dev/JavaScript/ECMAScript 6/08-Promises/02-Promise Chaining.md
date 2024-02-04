# Promise Chaining

## Introduction to the JavaScript promise chaining

有时，想要执行两个或多个相关的异步操作，其中下一个操作从上一步的结果开始。例如：

First, create a new promise that resolves to the number 10 after 3 seconds:

```js
let p = new Promise((resolve, reject) => {
    setTimeout(() => {
        resolve(10);
    }, 3 * 100);
});
```

> setTimeout() 函数模拟异步操作。

然后，调用 Promise 的 then() 方法：

```js
p.then((result) => {
    console.log(result);
    return result * 2;
});
```

The callback passed to the `then()` method executes once the promise is resolved. In the callback, we show the result of the promise and return a new value multiplied by two (`result*2`).

Because the `then()` method returns a new `Promise` with a value resolved to a value, you can call the `then()` method on the return `Promise` like this:

```js
let p = new Promise((resolve, reject) => {
    setTimeout(() => {
        resolve(10);
    }, 3 * 100);
});

p.then((result) => {
    console.log(result); // 10
    return result * 2;
}).then((result) => {
    console.log(result); // 20
    return result * 3;
}).then((result) => {
    console.log(result); // 60
    return result * 4;
});
```

这样调用 then() 方法的方式通常称为 promise chain。

<img src="D:\2024年\blogs\Web Dev\JavaScript\ECMAScript\07-Promise && async-await\assets\JavaScript-Promise-Chaining-17067593105245.png" alt="JavaScript Promise Chaining" style="zoom:50%;" />



## Multiple handlers for a promise

当对同一个 Promise 多次调用 then() 方法时，这不是 Promise 链。例如：

```js
let p = new Promise((resolve, reject) => {
    setTimeout(() => {
        resolve(10);
    }, 3 * 100);
});

p.then((result) => {
    console.log(result); // 10
    return result * 2;
})

p.then((result) => {
    console.log(result); // 10
    return result * 3;
})

p.then((result) => {
    console.log(result); // 10
    return result * 4;
});
```

In this example, we have multiple handlers for one promise. These handlers have no relationships. Also, they execute independently and don’t pass the result from one to another like the promise chain above.

![JavaScript Promise Chaining - multiple handlers](D:\2024年\blogs\Web Dev\JavaScript\ECMAScript\07-Promise && async-await\assets\JavaScript-Promise-Chaining-multiple-handlers.png)

In practice, you will rarely use multiple handlers for one promise.

## Returning a Promise

When you return a value in the `then()` method, the `then()` method returns a new `Promise` that immediately resolves to the return value.

另外，可以在 then() 方法中返回一个新的 Promise，如下所示：

```js
let p = new Promise((resolve, reject) => {
    setTimeout(() => {
        resolve(10);
    }, 3 * 100);
});

p.then((result) => {
    console.log(result);
    return new Promise((resolve, reject) => {
        setTimeout(() => {
            resolve(result * 2);
        }, 3 * 1000);
    });
}).then((result) => {
    console.log(result);
    return new Promise((resolve, reject) => {
        setTimeout(() => {
            resolve(result * 3);
        }, 3 * 1000);
    });
}).then(result => console.log(result));
```

下面对上面的例子进行修改：

```js
function generateNumber(num) {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve(num);
    }, 3 * 1000);
  });
}

generateNumber(10)
  .then((result) => {
    console.log(result);
    return generateNumber(result * 2);
  })
  .then((result) => {
    console.log(result);
    return generateNumber(result * 3);
  })
  .then((result) => console.log(result));
```

### Promise chaining syntax

> 这个例子多看看，比较复杂，不好理解

假设要按顺序执行以下异步操作：

- First, get the user from the database.
- Second, get the services of the selected user.
- Third, calculate the service cost from the user’s services.

以下函数说明了三种异步操作：

```js
function getUser(userId) {
    return new Promise((resolve, reject) => {
        console.log('Get the user from the database.');
        setTimeout(() => {
            resolve({
                userId: userId,
                username: 'admin'
            });
        }, 1000);
    })
}

function getServices(user) {
    return new Promise((resolve, reject) => {
        console.log(`Get the services of ${user.username} from the API.`);
        setTimeout(() => {
            resolve(['Email', 'VPN', 'CDN']);
        }, 3 * 1000);
    });
}

function getServiceCost(services) {
    return new Promise((resolve, reject) => {
        console.log(`Calculate the service cost of ${services}.`);
        setTimeout(() => {
            resolve(services.length * 100);
        }, 2 * 1000);
    });
}
```

The following uses the promises to serialize the sequences:

```js
getUser(100)
    .then(getServices)
    .then(getServiceCost)
    .then(console.log);
```

输出：

```js
Get the user from the database.
Get the services of admin from the API.
Calculate the service cost of Email,VPN,CDN.
300
```

> 注意，ES2017 引入了 async/await，可以编写比使用 Promise 链技术更干净的代码。