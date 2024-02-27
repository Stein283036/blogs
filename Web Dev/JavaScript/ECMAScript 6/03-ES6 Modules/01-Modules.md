# ES6 Modules

## Introduction to ES6 modules

在早期，JavaScript 最初服务于为网页提供交互性的小型脚本任务。如今，JavaScript 已经发展到可以为浏览器和服务器 (Node.js) 中的完整应用程序提供支持。

为了应对这种增长，有必要将 JavaScript 代码模块化为模块，并使它们可以跨应用程序重用。

ES6 引入了模块的概念。模块是在**严格模式下（strict mode）**执行的 JavaScript 文件。这意味着模块中声明的任何变量或函数都不会自动添加到全局范围（global scope）。

好消息是现代 Web 浏览器和 Node.js 支持原生 ES6 模块。这种原生支持简化了模块加载并优化了性能。

> ES6 modules are supported in Node. js versions 13 and above.

## ES6 modules example

创建一个具有以下目录和文件结构的新项目：

```js
├── index.html
└── js
   ├── index.js
   └── lib.js
```

首先，在 lib.js 模块中定义一个名为 display() 的函数：

```js
function display(message) {
  const el = document.createElement('div');
  el.innerText = message;
  document.body.appendChild(el);
}
```

display() 函数通过创建 div 元素并将其附加到 body 元素来在网页上显示 message。

其次，在 index.html 文件中加载 index.js 文件：

```html
<!DOCTYPE html>
<html lang="en">

    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>ES6 Modules</title>
    </head>

    <body>

        <script src="js/index.js"></script>
    </body>

</html>
```

要在 index.js 文件中使用 lib.js 文件的 display() 函数，可以使用 ES6 模块。

1. 使用 export 语句导出 lib.js 文件中的 display() 函数：`export { display }`

2. 使用 import 语句从 lib.js 模块导入 display 函数，并调用 display() 函数在网页上显示 Hi 消息：

   ```js
   import { display } from './lib.js';
   
   display('Hi');
   ```

3. 将 type="module" 添加到 index.html 中的脚本标记中，以指示 Web 浏览器将 index.js 文件作为模块加载：

   ```js
   <!DOCTYPE html>
   <html lang="en">
       <head>
           <meta charset="UTF-8">
           <meta name="viewport" content="width=device-width, initial-scale=1.0">
           <title>ES6 Modules</title>
       </head>
       <body>
   
           <script src="js/index.js" type="module"></script>
       </body>
   </html>
   ```