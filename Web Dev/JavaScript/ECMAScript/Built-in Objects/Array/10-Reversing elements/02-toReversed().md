# JavaScript Array toReversed

## Introduction to the JavaScript Array toReversed() method

The `toReversed()` method reverses the order of elements in an [array](https://www.javascripttutorial.net/javascript-array/) and returns a **new array** with the elements in reversed order.

Unlike the `reversed()` method that reverses the elements of the array in place, the `toReversed()` method does not modify the original array. Instead, it creates a new array with the elements of the original array in the reversed order.

```js
Array.prototype.toReversed()
```

The `toReversed()` method takes no parameters and returns a new array containing the elements in reversed order.

When you call the `toReversed()` method on a sparse array, it treats empty slots as if they have the value `undefined`.

This method is **generic**, meaning that you can call it on a non-array object that has a `length` property and integer-keyed properties.

## JavaScript Array toReversed() method examples

### Using JavaScript Array toReversed() method on string arrays

```js
const colors = ['red','green','blue'];
const reversedColors = colors.toReversed();
console.log(colors); // ['red','green','blue']
console.log(reversedColors); // ['blue', 'green', 'red']
```

### Using the JavaScript Array toReversed() method on number arrays

```js
const scores = [1, 3, 5, 7];
const reversedScores = scores.toReversed();
console.log(scores); // [1, 3, 5, 7]
console.log(reversedScores); // [7, 5, 3, 1]
```

### Using JavaScript Array toReversed() method on arrays of objects

```js
const contacts = [{name: 'John'}, {name: 'Alice'}, {name: 'Bob'}];
const reversedContacts = contacts.toReversed();
console.log(contacts); // [{name: 'John'}, {name: 'Alice'}, {name: 'Bob'}]
console.log(reversedContacts); // [{name: 'Bob'}, {name: 'Alice'}, {name: 'John'}]
```

### Calling toReversed() method on sparse arrays

When you call the `toReversed()` method on a sparse array, the result array remains sparse. The` toReversed()` method copies empty slots over their respective indices as empty slots:

```js
const scores = [1,,7,5];
const reversedScores = scores.toReversed();
console.log(scores); // [1,, 7, 5]
console.log(reversedScores); // [5, 7, undefined, 1]
```









