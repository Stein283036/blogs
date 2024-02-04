# Returning Multiple Values from a Function

JavaScript 函数可以返回单个值。要从函数返回多个值，可以将返回值打包为数组的元素或对象的属性。

## Returning multiple values from a function using an array

假设以下 getNames() 函数从后端数据库或第三方 API 调用的结果中检索名字和姓氏，并将它们作为数组元素返回：

```js
function getNames() {
    // get names from the database or API
    let firstName = 'John',
        lastName = 'Doe';

    // return as an array
    return [firstName, lastName];
}
```

下面展示了如何从 getNames() 函数获取返回值：

```js
let names = getNames();
```

由于名称变量是一个数组，因此可以使用方括号引用其元素，如下所示：

```js
const firstName = names[0],
      lastName  = names[1];
```

在 ES6 中，可以使用解构赋值语法更直观地从数组中解压值，如下所示：

```js
const [firstName, lastName] = getNames();
```

## Returning multiple values from an function using an object

如果要为每个返回值分配一个名称以使其更具可读性且更易于维护，可以使用对象：

```js
function getNames() {
  // get names from the database or API
  let firstName = 'John',
      lastName = 'Doe';

  // return values
  return {
      firstName,
      lastName
  };
}
```

可以像这样获取对象的返回值：

```js
let names = getNames();
let firstName = names.firstName,
    lastName  = names.lastName;
```

如果要从对象中解包属性，可以使用对象解构语法，如下所示：

```js
let { firstName, lastName } = getNames();
```