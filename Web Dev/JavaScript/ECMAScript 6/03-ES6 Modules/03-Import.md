# JavaScript Import

## Introduction to JavaScript import keyword

ES6 模块允许 JavaScript 代码构建为模块并在模块之间共享值（变量、函数、类等）。

要从模块导入值，使用 import 关键字。此外，还需要将 JavaScript 源文件作为模块加载。在 HTML 中，通过在 script 标签中指定 type="module" 来完成此操作：

```js
<script type="module" src="app.js"></script>
```

在 Node.js 中，在 package.json 文件中添加配置项：

```json
"type": "module"
```

有一个具有以下结构的项目：

```js
├── index.html
└── js
   ├── app.js
   └── greeting.js
```

在此项目中，index.html 将 app.js 作为模块加载：

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>JavaScript import</title>
    </head>
    <body>
        <script src="js/app.js" type="module"></script>
    </body>
</html>
```

greeting.js 模块有一个 sayHi() 函数，用于显示消息。它将 sayHi() 函数导出为默认导出：

```js
export default function sayHi() {
  alert('Hi');
}
```

app.js 将从 greeting.js 模块导入 sayHi() 方法并执行它。

## Import a default export

如果模块使用默认导出，使用以下语法从该模块导入默认导出：

```js
import name from 'module.js';
```

例如，可以将 sayHi() 函数从 greeting.js 模块导入到 app.js 模块，如下所示：

```js
import sayHi from './greeting.js';

sayHi();
```

由于 sayHi() 函数是默认导出函数，因此可以在导入时为其指定任何名称。

```js
import displayGreeting from './greeting.js';

displayGreeting();
```

## Import named exports

与导入默认导出不同，将命名导出导入到模块中时，需要指定它们的确切名称。此外，需要将命名导出放在一对大括号内。

导入命名导出的语法：

```js
import { namedExport1, namedExport2} from 'module.js';
```

例如，我们可以修改包含两个命名导出的 greeting.js 模块：

```js
export function sayHi() {
  alert('Hi');
}

export function sayBye() {
  alert('Bye');
}
```

将 sayHi 和 sayBye 两个命名导出函数导入到 app.js 模块：

```js
import { sayHi, sayBye } from './greeting.js'
```

## Namespace import

A module namespace object is a static object that includes all exports from a module. It is a static object that JavaScript creates when evaluating the module.

要访问模块命名空间对象，使用以下语法：

```js
import * as name from 'module.js';
```

在此语法中，name 是模块命名空间对象，其中包含 module.js 模块的所有导出作为属性。

例如，如果 module.js 具有 myVariable、myFunction 和 myClass 命名导出，则可以通过 name 对象访问它们，如下所示：

```js
name.myVariable
name.myFunction
name.myClass
```

为了说明命名空间导入的工作原理，更改 app.js 以使用命名空间导入，如下所示：

```js
import * as greeting from './greeting.js';

greeting.sayHi();
greeting.sayBye();
```

如果导入模块有默认导出，则可以通过 default 关键字访问它：

```js
name.default
```

例如，将 sayHi 函数更改为 greeting.js 模块中的默认导出：

```js
export default function sayHi() {
  alert('Hi');
}

export function sayBye() {
  alert('Bye');
}
```

并使用命名空间导入将 greeting.js 模块中的导出导入到 app.js 模块中：

```js
import * as greeting from './greeting.js';

greeting.default(); // sayHi()
greeting.sayBye();
```

## Renaming a named export

当导入命名导出时，可以为其指定一个新名称。当从不同模块导入具有相同名称的函数时，它很有用：

```js
import { name as name1 } from "module1.js";
import { name as name2 } from "module2.js";
```

例如，下面说明了在导入到 app.js 模块时如何将 sayHi() 和 sayBye() 函数重命名为 hi() 和 bye()：

```js
import { sayHi as hi, sayBye as bye } from './greeting.js';

hi();
bye();
```