# Understanding JavaScript Pass-By-Value

## JavaScript pass-by-value or pass-by-reference

在 JavaScript 中，所有函数参数始终按值传递。这意味着 JavaScript 将变量的值复制到函数参数中。

对函数内部参数所做的任何更改都不会反映函数外部的传递变量。换句话说，对参数所做的更改不会反映在函数外部。

如果函数参数通过引用传递，则传递到函数中的变量的更改将反映在函数外部。这在 JavaScript 中是不可能的。

## Pass-by-value of primitives values

## Pass-by-value of reference values

不明显看出引用值也是按值传递的。例如：

```js
let person = {
  name: 'John',
  age: 25,
};

function increaseAge(obj) {
  obj.age += 1;
}

increaseAge(person);

console.log(person);
```

JavaScript 似乎通过引用传递对象，因为对对象的更改反映在函数外部。然而，这种情况并非如此。

事实上，当将对象传递给函数时，传递的是该对象的引用，而不是实际的对象。因此，函数可以通过对象的引用来修改对象的属性。

但是，无法更改传递到函数中的引用。例如：

```js
let person = {
  name: 'John',
  age: 25,
};

function increaseAge(obj) {
  obj.age += 1;

  // reference another object
  obj = { name: 'Jane', age: 22 };
}

increaseAge(person);

console.log(person); // { name: 'John', age: 26 }
```

person 引用仍然引用 age 属性更改为 26 的原始对象。换句话说，increaseAge() 函数不会更改 person 引用。



