# JavaScript Array splice: Delete, Insert, and Replace

JavaScript Array type provides a very powerful `splice()` method that allows you to insert new elements into the middle of an array. Also, you can use this method to delete and replace existing elements as well.

## Deleting elements using JavaScript Array’s splice() method

```js
splice(start: number, deleteCount: number, ...items: number[]): number[]
// The zero-based location in the array from which to start removing elements.
// deleteCount: The number of elements to remove.
// items: Elements to insert into the array in place of the deleted elements.
// Removes elements from an array and, if necessary, inserts new elements in their place, returning the deleted elements.
```

```js
let scores = [1, 2, 3, 4, 5];
```

deletes three elements of the `scores` array starting from the first element.

```js
let deletedScores = scores.splice(0, 3);
console.log(scores); //  [4, 5]
console.log(deletedScores); // [1, 2, 3]
```

![JavaScript Array Splice Delete Example](D:\2024年\blogs\Web Dev\JavaScript\ECMAScript\Built-in Objects\JavaScript Array Methods\02-Addingremoving elements\assets\JavaScript-Array-Splice-Delete-Example.png)

## Inserting elements using the JavaScript Array splice() method

You can insert one or more elements into an array by passing three or more arguments to the `splice()` method with the second argument is **zero**.

```js
let colors = ['red', 'green', 'blue'];
colors.splice(2, 0, 'purple');
console.log(colors); // ["red", "green", "purple", "blue"]
colors.splice(1, 0, 'yellow', 'pink');
console.log(colors); // ["red", "yellow", "pink", "green", "purple", "blue"]
```

## Replacing elements using the JavaScript Array splice() method

```js
let languages = ['C', 'C++', 'Java', 'JavaScript'];
languages.splice(1, 1, 'Python');
console.log(languages); // ["C", "Python", "Java", "JavaScript"]
```

可以通过向 splice() 方法传递更多参数来将一个元素替换为多个元素：

```js
languages.splice(2, 1, 'C#', 'Swift', 'Go');
console.log(languages); // ["C", "Python", "C#", "Swift", "Go", "JavaScript"]
```