# JavaScript Callbacks

## What are callbacks

在 JavaScript 中，函数是一等公民。因此，可以将一个函数作为参数传递给另一个函数。

根据定义，回调是一个函数，可以将其作为参数传递给另一个函数以便稍后执行（定时任务、用户输入的事件处理等）。

下面定义了一个 filter() 函数，它接受一个数字数组并返回一个新的奇数数组：

```js
function filter(numbers) {
  let results = [];
  for (const number of numbers) {
    if (number % 2 != 0) {
      results.push(number);
    }
  }
  return results;
}
let numbers = [1, 2, 4, 7, 3, 5, 6];
console.log(filter(numbers));
```

如果要返回包含偶数的数组，则需要修改 filter() 函数。为了使 filter() 函数更加通用和可重用，可以：

- 首先，提取 if 块中的逻辑并将其包装在单独的函数中。
- 其次，将该函数作为实参（回调函数）传递给 filter() 函数。

```js
function isOdd(number) {
  return number % 2 != 0;
}
function isEven(number) {
  return number % 2 == 0;
}

function filter(numbers, fn) {
  let results = [];
  for (const number of numbers) {
    if (fn(number)) {
      results.push(number);
    }
  }
  return results;
}
let numbers = [1, 2, 4, 7, 3, 5, 6];

console.log(filter(numbers, isOdd));
console.log(filter(numbers, isEven));
```

根据定义，isOdd 和 isEven 是回调函数或回调。因为 filter() 函数接受一个函数作为参数，所以它被称为高阶函数（*high-order function*）。

回调可以是匿名函数，它是没有名称的函数，如下所示：

```js
function filter(numbers, callback) {
  let results = [];
  for (const number of numbers) {
    if (callback(number)) {
      results.push(number);
    }
  }
  return results;
}

let numbers = [1, 2, 4, 7, 3, 5, 6];

let oddNumbers = filter(numbers, function (number) {
  return number % 2 !== 0;
});

console.log(oddNumbers);
```

在此示例中，将匿名函数传递给 filter() 函数，而不是使用单独的函数。

在 ES6 中，可以使用这样的箭头函数：

```js
function filter(numbers, callback) {
  let results = [];
  for (const number of numbers) {
    if (callback(number)) {
      results.push(number);
    }
  }
  return results;
}

let numbers = [1, 2, 4, 7, 3, 5, 6];

let oddNumbers = filter(numbers, (number) => number % 2 !== 0);

console.log(oddNumbers);
```

回调有两种类型：同步回调和异步回调。

## Synchronous callbacks

同步回调是在使用回调的高阶函数在执行期间执行的。isOdd 和 isEven 是同步回调的示例，因为它们在 filter() 函数执行期间执行。

## Asynchronous callbacks

异步回调在使用回调的高阶函数执行后执行。

异步性意味着如果 JavaScript 必须等待某个操作完成，它将在等待期间执行其余的代码。

**JavaScript 是一种单线程（single-threaded）编程语言。它通过回调队列（callback queue）和事件循环（event loop）承载异步操作。**

假设需要开发一个脚本，从远程服务器下载图片并在下载完成后对其进行处理：

```js
function download(url) {
    // ...
}

function process(picture) {
    // ...
}

download(url);
process(picture);
```

但是，从远程服务器下载图片需要时间，具体取决于网络速度和图片大小。

下面的 download() 函数使用 setTimeout() 函数来模拟网络请求：

```js
function download(url) {
    setTimeout(() => {
        // script to download the picture here
        console.log(`Downloading ${url} ...`);
    },1000);
}
```

下面代码模拟 process() 函数：

```js
function process(picture) {
    console.log(`Processing ${picture}`);
}
```

当执行以下代码时：

```js
let url = 'https://www.javascripttutorial.net/pic.jpg';

download(url);
process(url);
```

将得到以下输出：

```js
Processing https://javascripttutorial.net/pic.jpg
Downloading https://javascripttutorial.net/pic.jpg ...
```

这不是所期望的，因为 process() 函数在 download() 函数之前执行。正确的顺序应该是：

- 下载图片并等待下载完成。
- 处理图片。

要解决此问题，可以将 process() 函数传递给 download() 函数，并在下载完成后执行 download() 函数内的 process() 函数，如下所示：

```js
function download(url, callback) {
    setTimeout(() => {
        // script to download the picture here
        console.log(`Downloading ${url} ...`);
        
        // process the picture once it is completed
        callback(url);
    }, 1000);
}

function process(picture) {
    console.log(`Processing ${picture}`);
}

let url = 'https://wwww.javascripttutorial.net/pic.jpg';
download(url, process);
// 输出
Downloading https://www.javascripttutorial.net/pic.jpg ...
Processing https://www.javascripttutorial.net/pic.jpg
```

现在，它按预期工作。

在此示例中，process() 是传递到异步函数的回调。

当在异步操作后使用回调继续执行代码时，该回调称为异步回调。

为了使代码更加简洁，可以将 process() 函数定义为匿名函数：

```js
function download(url, callback) {
    setTimeout(() => {
        // script to download the picture here
        console.log(`Downloading ${url} ...`);
        // process the picture once it is completed
        callback(url);

    }, 1000);
}

let url = 'https://www.javascripttutorial.net/pic.jpg';
download(url, function(picture) {
    console.log(`Processing ${picture}`);
}); 
```

### Handling errors

download() 函数假设一切正常并且不考虑任何异常。下面的代码引入了两个回调：success 和 failure，分别处理成功和失败的情况：

```js
function download(url, success, failure) {
  setTimeout(() => {
    console.log(`Downloading the picture from ${url} ...`);
    !url ? failure(url) : success(url);
  }, 1000);
}

download(
  '',
  (url) => console.log(`Processing the picture ${url}`),
  (url) => console.log(`The '${url}' is not valid`)
);
```

### Nesting callbacks and the Pyramid of Doom

如何下载三张图片并按顺序处理它们？典型的方法是在回调函数中调用 download() 函数，如下所示：

```js
function download(url, callback) {
  setTimeout(() => {
    console.log(`Downloading ${url} ...`);
    callback(url);
  }, 1000);
}

const url1 = 'https://www.javascripttutorial.net/pic1.jpg';
const url2 = 'https://www.javascripttutorial.net/pic2.jpg';
const url3 = 'https://www.javascripttutorial.net/pic3.jpg';

download(url1, function (url) {
  console.log(`Processing ${url}`);
  download(url2, function (url) {
    console.log(`Processing ${url}`);
    download(url3, function (url) {
      console.log(`Processing ${url}`);
    });
  });
});
```

输出：

```js
Downloading https://www.javascripttutorial.net/pic1.jpg ...
Processing https://www.javascripttutorial.net/pic1.jpg
Downloading https://www.javascripttutorial.net/pic2.jpg ...
Processing https://www.javascripttutorial.net/pic2.jpg
Downloading https://www.javascripttutorial.net/pic3.jpg ...
Processing https://www.javascripttutorial.net/pic3.jpg
```

该脚本运行得非常好。

然而，当复杂性显着增加时，这种回调策略就不能很好地扩展。

在回调中嵌套许多异步函数被称为厄运金字塔或回调地狱：

```js
asyncFunction(function(){
    asyncFunction(function(){
        asyncFunction(function(){
            asyncFunction(function(){
                asyncFunction(function(){
                    ....
                });
            });
        });
    });
});
```

为了避免回调地狱，可以使用 Promise 或 async/await 函数。