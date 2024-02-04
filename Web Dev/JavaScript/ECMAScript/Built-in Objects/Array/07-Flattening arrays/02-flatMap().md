# JavaScript Array flatMap

## Introduction to JavaScript Array `flatMap()` method

The `flatMap()` method is the combination of the `map()` method followed by the `flat()` method of depth 1.

The `flatMap()` method first maps each element in an array using a mapping function and then flattens the results into a new array.

flatMap() 方法的语法：

```js
flatMap(callback: (value: any, index: number, array: any[]) => any, thisArg?: undefined): any[]
// Calls a defined callback function on each element of an array. Then, flattens the result into a new array. This is identical to a map followed by flat with depth 1.
```

## JavaScript Array `flatMap()` examples

### Creating words from sentences example

```js
let sentences = ["JavaScript Array flatMap()", " ", "is", " ", "Awesome"];
```

The following `map()` function splits the words of sentences:

```js
let words = sentences.map(s => s.split(' '));
console.log(words);
```

输出：

```js
[
    [ 'JavaScript', 'Array', 'flatMap()' ],
    [ ' ' ],
    [ 'is' ],
    [ ' ' ],
    [ 'Awesome' ]
]
```

The result is an array of nested arrays filled by words. To flatten the result, you can use the `flat()` method on the result of the `map()` method. However, it’ll be more concise to use the `flatMap()` method.

```js
let sentences = [
    "JavaScript Array flatMap()", 
    " ", 
    "is", 
    " ", 
    "Awesome"
];
let words = sentences.flatMap(s => s.split(' '));
console.log(words); // [ 'JavaScript', 'Array', 'flatMap()', '', '', 'is', '', '', 'Awesome' ]
```

### Adding and removing elements during mapping example

The `flatMap()` method allows you to add or remove elements during mapping.

```js
let cart = [
  {
    name: 'Smartphone',
    qty: 2,
    price: 500,
    freeOfCharge: false,
  },
  {
    name: 'Tablet',
    qty: 1,
    price: 800,
    freeOfCharge: false,
  },
]
```

If customers buy a smartphone, you want to give them a free screen protector.

When the customer adds a smartphone to the cart, you can add a screen protector to the cart using the `flatMap()` method as follows:

```js
let newCart = cart.flatMap(
    (item) => {
        if (item.name === 'Smartphone') {
            return [item, {
                name: 'Screen Protector',
                qty: item.qty,
                price: 5,
                freeOfCharge: true
            }]
        } else {
            return [item];
        }
    }
);
console.log(newCart);
```

输出：

```js
[
    { name: 'Smartphone', qty: 2, price: 500, freeOfCharge: false },
    { name: 'Screen Protector', qty: 2, price: 5, freeOfCharge: true },
    { name: 'Tablet', qty: 1, price: 800, freeOfCharge: false }
]
```

The following uses the `reduce()` method to calculate the total amount from the items in the cart. It ignores the free-of-charge items, like screen protectors:

```js
const total = newCart.reduce((sum, item) => {
    if (!item.freeOfCharge)
        sum += item.price * item.qty;
    return sum;
}, 0);
console.log({total}); // { total: 1800 }
```