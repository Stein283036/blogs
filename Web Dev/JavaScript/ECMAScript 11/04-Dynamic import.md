# JavaScript Dynamic Import

## Introduction to the JavaScript dynamic import

有一个具有以下结构的项目：

```
├── index.html
└── js
   ├── app.js
   └── greeting.js
```

index.html 从 js 目录加载 app.js 文件。 index.html 包含一个按钮，如果单击该按钮（动态条件），才会显示警报：

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>JavaScript Dynamic Import</title>
    </head>
    <body>
        <input type="button" value="Click Me" class="btn">
        <script src="js/app.js" type="module"></script>
    </body>
</html>
```

greeting.js 模块定义了 sayHi() 函数并使用命名导出将其导出：

```js
export function sayHi() {
  alert('Hi');
}
```

app.js 模块从 greeting.js 模块导入 sayHi 函数。它选择类为 .btn 的按钮，并在单击按钮时调用 sayHi() 函数：

```js
import { sayHi } from './greeting.js';

const btn = document.querySelector('.btn');
btn.addEventListener('click', () => {
  sayHi();
});
```

在 ES2020 之前，无法在需要时动态加载 greeting.js 模块。

例如，以下 app.js 模块仅在单击按钮时尝试加载 greeting.js 模块并导致错误：

```js
const btn = document.querySelector('.btn');

btn.addEventListener('click', () => {
  import sayHi from './greeting.js'; // ERROR
  sayHi();
});
```

ES2020 通过类似函数的 import() 引入了模块的动态导入，语法如下：

```js
import(moduleSpecifier);
```

import() 允许在需要时动态导入模块。

import() 的工作原理如下：

- import() 接受一个模块说明符 (moduleSpecifier)，其格式与用于 import 语句的模块说明符相同。此外， moduleSpecifier 可以是计算结果为字符串的表达式。
- import() 返回一个 Promise，一旦模块完全加载，该 Promise 的状态就变为 fulfilled。

下面说明了如何使用 import() 语法从 app.js 模块动态加载greeting.js 模块：

```js
const btn = document.querySelector('.btn');

btn.addEventListener('click', () => {
  import('./greeting.js')
    .then((greeting) => {
      greeting.sayHi();
    })
    .catch((error) => {
      console.error(error);
    });
});
```

由于 import() 返回 Promise，因此可以在 app.js 模块中使用 async/await，如下所示：

```js
const btn = document.querySelector('.btn');

btn.addEventListener('click', async () => {
  try {
    let greeting = await import('./greeting.js');
    greeting.sayHi();
  } catch (error) {
    console.log(error);
  }
});
```

## Some practical use cases of JavaScript import()

### Loading module on demand

应用程序启动时某些模块可能不需要可用。为了缩短加载时间，可以将此类功能放置在模块中，并使用 import() 按需加载它们，如下所示：

```js
function eventHandler() {
    import('./module1.js')
        .then((ns) => {
            // use the module 
            ns.func();
        })
        .catch((error) => {
            // handle error
        });
}
```

### Loading modules based on conditions

当将 import() 放在条件语句（例如 if-else）中时，可以根据特定条件加载模块。

```js
if( isSpecificPlatform() ) {
    import('./platform.js')
    .then((ns) => {
        ns=>f();
    });
}
```

### Computed module specifiers

module specifier 是一个表达式，决定了在运行时加载哪个模块。

例如，可以根据用户的区域设置加载模块，以用户的特定语言显示消息：

```js
let lang = `message_${getUserLocale()}.js`;

import(lang)
    .then(...);
```

### Dynamically loading multiple modules

要动态加载多个模块，可以使用 Promise.all() 方法：

```js
Promise.all([
    import(module1), 
    import(module2),
    ])
    .then(([module1,module2]) => {
        // use the modules
    });
```