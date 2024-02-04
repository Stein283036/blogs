# JavaScript Array Reverse

## Introduction to JavaScript Array Reverse method

The `reverse()` method reverses the order of elements within the array and returns the modified array with elements in the reversed order.

reverse() 方法的语法：

```js
reverse(): any[]
// Reverses the elements in an array in place. This method mutates the array and returns a reference to the same array.
```

The `reverse()` method is **generic**. This means that you can call it on a non-array object that has the `length` property and integer-keyed properties.

> Note that you cannot call the `reverse()` on strings because strings are **immutable**.

## JavaScript Array reverse() method examples

### Using JavaScript array reverse() method on string arrays

```js
const colors = ['red','green','blue'];
colors.reverse();
console.log(colors); // ['blue', 'green', 'red']
```

### Using the JavaScript array reverse() method on number arrays

```js
const scores = [1, 3, 5, 7];
scores.reverse();
console.log(scores); // [7, 5, 3, 1]
```

### Using JavaScript array reverse() method on arrays of objects

```js
const books = [
  { title: 'Eloquent JavaScript', author: 'Marijn Haverbeke' },
  { title: 'JavaScript: The Good Parts', author: 'Douglas Crockford' },
  { title: 'JavaScript: The Definitive Guide', author: 'David Flanagan' },
]
books.reverse()
console.log(books)
```

### Using reverse() on sparse arrays

When you call the `reverse()` method on a sparse array, the array remains sparse. The `reverse()` method copies empty slots over their respective indices as empty slots:

```js
const scores = [1,,7,5];
scores.reverse();
console.log(scores); // [5, 7, empty, 1]
```