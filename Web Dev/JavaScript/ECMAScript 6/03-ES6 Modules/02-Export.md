# JavaScript Export

## Introduction to JavaScript export keyword

ES6 模块允许以模块化方式构建 JavaScript 代码。模块提供了一种在 JavaScript 应用程序中定义和导入/导出可重用代码片段的标准化方法。

默认情况下，ES6 模块封装其代码。这意味着默认情况下无法从模块外部访问模块中定义的值（变量 variables、函数 functions、类 classes 等）。这可以防止命名冲突并促进更好的代码结构。

模块可以使用 export 关键字导出值（变量、函数、类等）。

export 导出有两种格式：

- named exports 命名导出
- default exports 默认导出

一个模块可以有多个命名导出，但只能有一个默认导出。

## Named exports

一个模块可以有多个命名导出。实践中，当需要从模块导出多个值时，可以使用命名导出。

### Exporting variables

```js
let count = 1;
export { count };
```

可以将变量声明和导出组合在一个语句中：

```js
export let count = 1;
```

同样，可以导出使用 const 关键字声明的变量：

```js
export const MIN = 0;
```

要导出多个变量，使用逗号 (,) 分隔它们：

```js
let count = 1;
const MIN = 0, MAX = 10;
export { count, MIN, MAX };
```

### Exporting functions

```js
function increase() {
  // ..
}
export { increase };
```

```js
export function increase() {
  // ...
}
```

### Exporting classes

```js
class Counter {
  constructor() {
    this.count = 1;
  }
  increase() {
    this.count++;
  }
  get current() {
    return this.count;
  }
}

export { Counter };
```

```js
export class Counter {
  constructor() {
    this.count = 1;
  }
  increase() {
    this.count++;
  }
  get current() {
    return this.count;
  }
}
```

导入命名导出时，需要使用确切的名称并在 {} 中指定它们。

```js
import { Counter } from 'module.js';
```

## Default exports

一个模块最多只有一个默认导出。要使用默认导出导出值，使用 export default 关键字。

```js
export default let message = 'Hi';
```

导入默认导出时，不需要将变量放在 {} 内：

```js
import message from 'module.js';
```

同样，可以使用默认导出从模块导出函数或类：

```js
export default function increase() {
   // ..
}

export default class Counter {
   // ...
}
```

## Renaming named exports

使用命名导出导出值时，可以将其重命名：

```js
class Counter {
  // ..
}

export { Counter as MyCounter };
```

导入时重命名：

```js
import { Counter as MyCounter } from 'module.js';
```

## Re-exporting

一个模块可以从另一个模块导入值并立即导出它们，如下所示：

```js
import { Counter } from 'module.js';
export { Counter };
```

使用导出语法来简化上述语法：

```js
export { Counter } from 'module.js';
```