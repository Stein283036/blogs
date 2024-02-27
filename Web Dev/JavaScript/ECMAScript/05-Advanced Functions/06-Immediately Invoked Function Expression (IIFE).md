# JavaScript Immediately Invoked Function Expression

JavaScript 立即调用函数表达式是定义为表达式并在创建后立即执行的函数。下面显示了定义立即调用函数表达式的语法：

```js
(function() {
    
})();
```

## Why IIFEs

当定义函数时，JavaScript 引擎会将该函数添加到全局对象中。

```js
function add(a,b) {
    return a + b;
}
```

在 Web 浏览器中，JavaScript 引擎将 add() 函数添加到 window 全局对象：

```js
console.log(window.add);
```

同样，如果使用 var 关键字在函数外部声明变量，JavaScript 引擎也会将该变量添加到全局对象中：

```js
var counter = 10;
console.log(window.counter); // 10
```

如果有很多全局变量和函数，JavaScript 引擎只会释放为它们分配的内存直到全局对象失去其作用域。

因此，脚本可能无法有效地使用**内存**。最重要的是，拥有全局变量和函数可能会导致**名称冲突**。

防止函数和变量污染全局对象的一种方法是使用立即调用的函数表达式。

在 JavaScript 中，可以使用以下表达式：

```js
'This is a string';
(10+20);
```

即使表达式没有效果，此语法也是正确的。函数也可以声明为表达式，称为函数表达式：

```js
let sum = function(a, b) {
    return a + b;
}
```

在此语法中，赋值运算符（=）右侧的部分是函数表达式。因为函数是一个表达式，所以可以将其括在括号内：

```js
let sum = (function(a, b) {
    return a + b;
});
```

在此示例中，sum 变量被引用为添加两个参数的匿名函数。

此外，可以在创建函数后立即执行该函数：

```js
let sum = (function(a,b){
    return a + b;
})(10, 20);

console.log(sum); // 30
```

在此示例中，sum 变量保存函数调用的结果。

以下表达式称为立即调用函数表达式 (IIFE)，因为该函数是作为表达式创建并立即执行的：

```js
(function(a,b){
    return a + b;
})(10,20);
```

这是定义 IIFE 的一般语法：

```js
(function () {
    
})();
```

请注意，可以使用箭头函数来定义 IIFE：

```js
(() => {
    
}))();
```

通过将函数和变量放置在立即调用的函数表达式中，可以避免将它们污染到全局对象：

```js
(function() {
    var counter = 0;

    function add(a, b) {
        return a + b;
    }

    console.log(add(10,20)); // 30
}());
console.log(window.counter); // undefined
```

## Named IIFE

IIFE 可以有一个名称。但执行后无法再次调用：

```js
(function namedIIFE() {
    //...
})();
```

## IIFE starting with a semicolon (;)

有时，可能会看到以分号 (;) 开头的 IIFE：

```js
;(function() {
/* */
})();
```

在此语法中，分号用于终止语句，以防两个或多个 JavaScript 文件被盲目连接成一个文件。

例如，可能有两个使用 IIFE 的文件 lib1.js 和 lib2.js：

```js
(function(){
    // ...
})()


(function(){
    // ...
})()
```

如果使用代码 bundler tool 将两个文件中的代码连接到一个文件中，如果没有分号 (;)，则连接的 JavaScript 代码将导致语法错误。

## IIFE in actions

假设有一个名为 calculator.js 的库，具有以下功能：

```js
function add(a, b) {
    return a + b;
}

function mutiply(a, b) {
    return a * b;
}
```

然后将 calculator.js 加载到 HTML 文档中。

稍后，还想将另一个名为 app.js 的 JavaScript 库加载到同一文档中：

```js
<!DOCTYPE html>
<head>
  <meta charset="UTF-8">
  <title>JavaScript IIFE</title>
</head>
<body>
  <script src="calculator.js"></script>
  <script src="app.js"></script>
</body>
</html>
```

app.js 也有 add() 函数：

```js
function add() {
    return 'add';
}
```

当在 HTML 文档中使用 add() 函数时，它返回“add”字符串而不是两个数字的和：

要解决此问题，可以在 calculator.js 中应用 IIFE，如下所示：

```js
const calculator = (function () {
    function add(a, b) {
        return a + b;
    }

    function multiply(a, b) {
        return a * b;
    }
    return {
        add: add,
        multiply: multiply
    }
})();
```

IIFE 返回一个对象，其中包含引用 add() 和 multiply() 函数的 add 和 multiply 方法。

在HTML文档中，可以使用 calculator.js 库，如下所示：

```html
<!DOCTYPE html>
<head>
  <meta charset="UTF-8">
  <title>JavaScript IIFE</title>
</head>
<body>
  <script src="js/calculator.js"></script>
  <script src="js/app.js"></script>
  <script>
    let result = calculator.add(10, 20); // add in calculator.js
    console.log(result); // 30
    console.log(add()); // add in the app.js
  </script>
</body>
</html>
```

calculator.add() 调用了 calculator.js 导出的 对象方法 add()，而对 add() 函数的第二次调用引用了 app.js 中的 add() 函数。

## jQuery & IIFE

以下 HTML 文档使用 jQuery 库：

```html
<!DOCTYPE html>
<head>
  <meta charset="UTF-8">
  <title>JavaScript IIFE - jQuery</title>
</head>
<body>
  <h1>jQuery Demo</h1>
  <script src="https://code.jquery.com/jquery-3.4.1.slim.js"
    integrity="sha256-BTlTdQO9/fascB1drekrDVkaKd9PkwBymMlHOiG+qLI=" crossorigin="anonymous"></script>
  <script>
    let counter = 1;
    $('h1').click(function () {
      $(this).text('jQuery Demo' + ' Clicked ' + counter++);
    });
  </script>
</body>
</html>
```

当导入 jQuery 库时，可以通过 $ 或 jQuery 函数对象访问许多有用的 jQuery 函数。在底层，jQuery 使用 IIFE 来暴露其功能。

通过这样做，jQuery 只需要使用一个全局变量 ($) 来暴露大量函数，而不会污染全局对象。
