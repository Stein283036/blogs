# JavaScript Array sort: Sorting Array Elements

## Introduction to JavaScript Array `sort()` method

sort() 方法允许对数组的元素进行就地（in place）排序。除了返回排序后的数组之外，sort() 方法还会更改原始数组中元素的位置。

默认情况下，sort() 方法按升序对数组元素进行排序，即最小值在前，最大值在后。

The `sort()` method casts elements to strings and compares the strings to determine the orders.

```js
let numbers = [0, 1 , 2, 3, 10, 20, 30 ];
numbers.sort();
console.log(numbers); // [ 0, 1, 10, 2, 20, 3, 30 ]
```

在此示例中，sort() 方法将 10 放在 2 之前，因为在进行字符串比较时，字符串“10”位于“2”之前。

要解决此问题，需要将比较函数传递给 sort() 方法。 sort() 方法将使用比较函数来确定元素的顺序。

sort() 方法的语法：

```js
sort(compareFn?: (a: any, b: any) => number): any[]
// compareFn: Function used to determine the order of the elements. It is expected to return a negative value if the first argument is less than the second argument, zero if they're equal, and a positive value otherwise. If omitted, the elements are sorted in ascending, ASCII character order.
// Sorts an array in place. This method mutates the array and returns a reference to the same array.
```

如果省略 compare function，sort() 方法将按照前面提到的基于元素的 Unicode code point 值的排序顺序对元素进行排序。

Compare() 函数接受两个参数 a 和 b。 sort() 方法将根据compare() 函数的返回值对元素进行排序，规则如下：

```js
let numbers = [0, 1, 2, 3, 10, 20, 30]
numbers.sort(function (a, b) {
  if (a > b) return 1
  if (a < b) return -1
  return 0
})
console.log(numbers) // [ 0, 1, 2, 3, 10, 20, 30 ]
```

```js
let numbers = [0, 30, 2, 15, 10, 20, 30]
numbers.sort((a, b) => a - b)
console.log(numbers) // [0, 2, 10, 15, 20, 30, 30]
```

## Sorting an array of strings

```js
let animals = [
    'cat', 'dog', 'elephant', 'bee', 'ant'
];
```

按字母升序对 Animals 数组的元素进行排序：

```js
let animals = [
    'cat', 'dog', 'elephant', 'bee', 'ant'
];
animals.sort();
console.log(animals); // [ 'ant', 'bee', 'cat', 'dog', 'elephant' ]
```

降序对动物数组进行排序：

```js
let animals = [
    'cat', 'dog', 'elephant', 'bee', 'ant'
];
animals.sort((a, b) => {
    if (a > b)
        return -1;
    if (a < b)
        return 1;
    return 0;
});
console.log(animals); // [ 'elephant', 'dog', 'cat', 'bee', 'ant' ]
```

### Sorting an array of strings with non-ASCII characters

sort() 方法可以很好地处理包含 ASCII 字符的字符串。但是，对于包含非 ASCII 字符的字符串，例如 é、è 等，sort() 方法将无法正常工作。

```js
let animaux = ['zèbre', 'abeille', 'écureuil', 'chat'];
animaux.sort();
console.log(animaux); // [ 'abeille', 'chat', 'zèbre', 'écureuil' ]
```

要解决此问题，可以使用 String 对象的 localeCompare() 方法来比较特定区域设置中的字符串，如下所示：

To resolve this, you use the `localeCompare()` method of the `String` object to compare strings in a specific locale:

```js
animaux.sort(function (a, b) {
    return a.localeCompare(b);
});
console.log(animaux); // [ 'abeille', 'chat', 'écureuil', 'zèbre' ]
```

## Sorting an array of objects by a specified property

The following is an array of `employee` objects, where each object contains three properties: `name`,`salary` and `hireDate`.

```js
let employees = [
    {name: 'John', salary: 90000, hireDate: "July 1, 2010"},
    {name: 'David', salary: 75000, hireDate: "August 15, 2009"},
    {name: 'Ana', salary: 80000, hireDate: "December 12, 2011"}
];
```

### Sorting objects by a numeric property

```js
// sort by salary
employees.sort(function (x, y) {
    return x.salary - y.salary;
});
console.table(employees);
```

### Sorting objects by a string property

```js
employees.sort((e1, e2) =>
  e1.name.toLocaleLowerCase().localeCompare(e2.name.toLocaleLowerCase())
)
console.log(employees)
```

### Sorting objects by the date property

To sort employees by hire date, you first have to create a valid Date object from the date string, and then compare two dates, which is the same as comparing two numbers.

```js
let employees = [
  { name: 'John', salary: 90000, hireDate: 'July 1, 2010' },
  { name: 'David', salary: 75000, hireDate: 'August 15, 2009' },
  { name: 'Ana', salary: 80000, hireDate: 'December 12, 2011' },
]
employees.sort((e1, e2) => new Date(e1.hireDate) - new Date(e2.hireDate))
console.log(employees)
```

## Optimizing JavaScript Array `sort()` method

In fact, the `sort()` method calls the compare function multiple times for each element in the array.

```js
let rivers = ['Nile', 'Amazon', 'Congo', 'Mississippi', 'Rio-Grande'];
rivers.sort(function (a, b) {
    console.log(a, b);
    return a.length - b.length;
});
```

输出：

```js
Amazon Nile
Congo Amazon
Congo Amazon
Congo Nile
Mississippi Congo
Mississippi Amazon
Rio-Grande Amazon
Rio-Grande Mississippi
```

How it works:

1. First, declare an array `rivers` that consists of the famous river names.
2. Second, sort the `rivers` array by the length of its element using the `sort()` method. We output the elements of the `rivers` array to the web console whenever the `sort()` method invokes the comparison function.

As shown in the output above, each element has been evaluated multiple times e.g., Amazon 4 times, Congo 2 times, etc.

If the number of array elements is increasing, it will potentially decrease the performance.

You cannot reduce the number of times that comparison function is executed. However, you can reduce the work that the comparison has to do. This technique is called [Schwartzian Transform](https://en.wikipedia.org/wiki/Schwartzian_transform).

To implement this, you follow these steps:

1. First, extract the actual values into a temporary array using the [map()](https://www.javascripttutorial.net/javascript-array-map/) method.
2. Second, sort the temporary array with the elements that are already evaluated (or transformed).
3. Third, walk the temporary array to get an array with the right order.

```js
let rivers = ['Nile', 'Amazon', 'Congo', 'Mississippi', 'Rio-Grande']
let lengths = rivers.map(function (e, i) {
  return { index: i, value: e.length }
})
lengths.sort((a, b) => a.value - b.value)
console.log(lengths)
let sortedRivers = lengths.map((value) => rivers[value.index])
console.log(sortedRivers) // [ 'Nile', 'Congo', 'Amazon', 'Rio-Grande', 'Mississippi' ]
```