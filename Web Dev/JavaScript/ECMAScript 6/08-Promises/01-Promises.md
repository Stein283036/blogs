# JavaScript Promises

## Why JavaScript promises

以下示例定义了一个返回用户对象数组的函数 getUsers()：

```js
function getUsers() {
  return [
    { username: 'john', email: 'john@test.com' },
    { username: 'jane', email: 'jane@test.com' },
  ];
}
```

每个 user 对象都有两个属性 username 和 email。

要从 getUsers() 函数返回的用户列表中按用户名查找用户，可以使用 findUser() 函数，如下所示：

```js
function findUser(username) {
  const users = getUsers();
  const user = users.find((user) => user.username === username);
  return user;
}
console.log(findUser('john')); // { username: 'john', email: 'john@test.com' }
```

findUser() 函数中的代码是同步且阻塞（synchronous and blocking）的。 findUser()函数执行getUsers()函数获取 users 数组，在 users 数组上调用 find() 方法来搜索具有特定用户名的用户，并返回匹配的用户。

在实际应用中，getUsers()函数可以访问数据库或者调用API来获取用户列表。因此，getUsers()函数会有延迟。

要模拟延迟，可以使用 setTimeout() 函数。例如：

```js
function getUsers() {
  let users = [];

  // delay 1 second (1000ms)
  setTimeout(() => {
    users = [
      { username: 'john', email: 'john@test.com' },
      { username: 'jane', email: 'jane@test.com' },
    ];
  }, 1000);

  return users;
}
```

getUsers() 将无法正常工作并且始终返回一个空数组。因此，findUser() 函数将无法按预期工作：

```js
function getUsers() {
  let users = [];
  setTimeout(() => {
    users = [
      { username: 'john', email: 'john@test.com' },
      { username: 'jane', email: 'jane@test.com' },
    ];
  }, 1000);
  return users;
}

function findUser(username) {
  const users = getUsers(); // A
  const user = users.find((user) => user.username === username); // B
  return user;
}

console.log(findUser('john')); // undefined
```

由于 getUsers() 返回一个空数组，因此 users 数组为空（A 行）。当对 users 数组调用 find() 方法时，该方法返回 undefined（B 行）。

挑战在于如何在一秒后访问从 getUsers() 函数返回的用户。一种经典的方法是使用回调。

### Using callbacks to deal with an asynchronous operation

以下示例将回调参数添加到 getUsers() 和 findUser() 函数：

```js
function getUsers(callback) {
  setTimeout(() => {
    callback([
      { username: 'john', email: 'john@test.com' },
      { username: 'jane', email: 'jane@test.com' },
    ])
  }, 1000)
}

function findUser(username, callback) {
  getUsers((users) => {
    const user = users.find((user) => user.username === username)
    callback(user)
  })
}

findUser('john', console.log) // { username: 'john', email: 'john@test.com' }
```

在此示例中， getUsers() 函数接受回调函数作为参数，并使用 setTimeout() 函数内的 users 数组调用它。此外，findUser() 函数接受处理匹配用户的回调函数。

回调方法效果很好。然而，它使代码更难以遵循。此外，它还增加了带有回调参数的函数的复杂性。

如果回调函数数量增加，会遇到回调地狱问题。为了解决这个问题，JavaScript 提出了 Promise 的概念。

## Understanding JavaScript Promises

根据定义，Promise 是一个封装**异步操作**结果的**对象**。

Promise 对象的状态可以是以下之一：

- Pending
- Fulfilled with a **value**
- Rejected for a **reason**

一开始，promise 的状态是pending，表示异步操作正在进行中。根据异步操作的结果，状态会更改为 fulfilled 或 rejected。

## Creating a promise

要创建 Promise 对象，使用 Promise() 构造函数：

```js
const promise = new Promise((resolve, reject) => {
  // contain an operation
  // ...

  // return the state
  if (success) {
    resolve(value);
  } else {
    reject(error);
  }
});
```

Promise 构造函数接受通常执行异步操作的回调函数。该函数通常称为执行器（executor）。

executor 依次接受两个名为resolve 和reject 的回调函数。

> 请注意，传递到执行器的回调函数仅按照约定命名为 resolve 和 reject

如果异步操作成功完成，executor 将调用 resolve() 函数将 promise 的状态从 pending 更改为 fulfilled 并有值。

如果发生错误，executor 将调用 reject() 函数将 promise 的状态从 pending 更改为 rejected，并给出错误原因。

一旦 Promise 达到 fulfilled 或 rejected 状态，它就会保持在该状态并且无法进入另一个状态。

换句话说，promise 不能从 fulfilled 状态变为 rejected 状态，反之亦然。此外，它无法从 fulfilled 或 rejected 状态返回到 pending 状态。

![img](https://www.javascripttutorial.net/wp-content/uploads/2022/02/JavaScript-Promises.svg)

> 注意，在实践中很少会创建 Promise 对象。相反，将使用库提供的 Promise，比如 axios。

## Consuming a Promise: then, catch, finally

### The then() method

要在 fulfiiled 状态获取 Promise 的值，可以调用 Promise 对象的 then() 方法。

```js
promise.then(onFulfilled,onRejected);
```

then() 方法接受两个回调函数：onFulfilled 和 onRejected。

如果 Promise 成功执行即为 fulfilled，那么 then() 方法会调用带值的 onFulfilled() 方法；如果 Promise 被拒绝即为 rejected，则调用 onRejected() 并返回错误。

> onFulfilled 和 onRejected 参数都是可选的。

以下示例显示如何使用 getUsers() 函数返回的 Promise 对象的 then() 方法：

```js
function getUsers() {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve([
        { username: 'john', email: 'john@test.com' },
        { username: 'jane', email: 'jane@test.com' },
      ]);
    }, 1000);
  });
}

function onFulfilled(users) {
  console.log(users);
}

const promise = getUsers();
promise.then(onFulfilled);
```

输出：

```js
[
  { username: 'john', email: 'john@test.com' },
  { username: 'jane', email: 'jane@test.com' }
]
```

为了使代码更加简洁，可以使用箭头函数作为 then() 方法的参数：

```js
function getUsers() {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve([
        { username: 'john', email: 'john@test.com' },
        { username: 'jane', email: 'jane@test.com' },
      ]);
    }, 1000);
  });
}

const promise = getUsers();

promise.then((users) => {
  console.log(users);
});
```

因为 getUsers() 函数返回一个 Promise 对象，所以可以将函数调用与 then() 方法链接起来，如下所示：

```js
// getUsers() function
//...

getUsers().then((users) => {
  console.log(users);
});
```

在此示例中，getUsers() 函数始终成功。为了模拟错误，可以使用如下所示的成功标志：

```js
// let success = true;
let success = false;

function getUsers() {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      if (success) {
        resolve([
          { username: 'john', email: 'john@test.com' },
          { username: 'jane', email: 'jane@test.com' },
        ]);
      } else {
        reject('Failed to the user list');
      }
    }, 1000);
  });
}

function onFulfilled(users) {
  console.log(users);
}
function onRejected(error) {
  console.log(error);
}

const promise = getUsers();
promise.then(onFulfilled, onRejected);
```

下面展示了如何使用箭头函数作为 then() 方法的参数：

```js
// getUsers() function
// ...

const promise = getUsers();
promise.then(
  (users) => console.log,
  (error) => console.log
);
```

### The catch() method

如果只想在 Promise 的状态是 rejected 时才获取错误，可以使用 Promise 对象的 catch() 方法：

```js
promise.catch(onRejected);
```

在内部，catch() 方法调用 then(undefined, onRejected) 方法。

以下示例将成功标志更改为 false 以模拟错误场景：

```js
let success = false;

promise.catch((error) => {
  console.log(error);
});
```

### The finally() method

有时，无论承诺是 fulfilled 还是 rejected，都希望执行同一段代码。例如：

```js
const render = () => {
  //...
};

getUsers()
  .then((users) => {
    console.log(users);
    render();
  })
  .catch((error) => {
    console.log(error);
    render();
  });
```

正如所看到的，render() 函数调用在 then() 和 catch() 方法中都是重复的。

要删除此重复项并执行 render() （无论 Promise 是 fulfilled 还是 rejected），可以使用 finally() 方法，如下所示：

```js
const render = () => {
  //...
};

getUsers()
  .then((users) => {
    console.log(users);
  })
  .catch((error) => {
    console.log(error);
  })
  .finally(() => {
    render();
  });
```

## A practical JavaScript Promise example

以下示例演示如何从服务器加载 JSON 文件并在网页上显示其内容。

假设有以下 JSON 文件及内容：

```js
https://www.javascripttutorial.net/sample/promise/api.json

{
    "message": "JavaScript Promise Demo"
}
```

下面显示了包含按钮的 HTML 页面。单击该按钮时，页面会从 JSON 文件加载数据并显示 message：

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8">
    <title>JavaScript Promise Demo</title>
    <link href="css/style.css" rel="stylesheet">
</head>
<body>
    <div id="container">
        <div id="message"></div>
        <button id="btnGet">Get Message</button>
    </div>
    <script src="js/promise-demo.js">
    </script>
</body>
</html>
```

下面展示了promise-demo.js文件：

```js
function load(url) {
  return new Promise(function (resolve, reject) {
    const request = new XMLHttpRequest();
    request.onreadystatechange = function () {
      if (this.readyState === 4 && this.status == 200) {
        resolve(this.response);
      } else {
        reject(this.status);
      }
    };
    request.open('GET', url, true);
    request.send();
  });
}

const url = 'https://www.javascripttutorial.net/sample/promise/api.json';
const btn = document.querySelector('#btnGet');
const msg = document.querySelector('#message');

btn.addEventListener('click', () => {
  load(URL)
    .then((response) => {
      const result = JSON.parse(response);
      msg.innerHTML = result.message;
    })
    .catch((error) => {
      msg.innerHTML = `Error getting the message, HTTP status: ${error}`;
    });
});
```