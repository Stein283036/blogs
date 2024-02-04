# JavaScript Array filter: Filtering Elements

## Introduction to JavaScript array `filter()` method

One of the most common tasks when working with an array is to create a new array that contains a subset of elements of the original array.

Suppose you have an array of city objects where each object contains two properties: `name` and `population`.

```js
let cities = [
    {name: 'Los Angeles', population: 3792621},
    {name: 'New York', population: 8175133},
    {name: 'Chicago', population: 2695598},
    {name: 'Houston', population: 2099451},
    {name: 'Philadelphia', population: 1526006}
];
```

find the city whose population is greater than 3 million:

```js
let bigCities = cities.filter(function (city) {
    return city.population > 3000000;
});
console.log(bigCities);

let bigCities = cities.filter(city => city.population > 3000000);
console.log(bigCities);
```

The `filter()` method includes the only elements in the result array if they satisfy the test in the callback function.

## JavaScript Array filter() method in detail

```js
filter(predicate: (value: any, index: number, array: any[]) => value is any, thisArg?: any): any[]
// predicate: A function that accepts up to three arguments. The filter method calls the predicate function one time for each element in the array.
// thisArg: An object to which the this keyword can refer in the predicate function. If thisArg is omitted, undefined is used as the this value.
// Returns the elements of an array that meet the condition specified in a callback function.
```

在内部，filter() 方法会迭代数组的每个元素，并将每个元素传递给回调函数。如果回调函数返回 true，则会将该元素包含在返回数组中。

## More JavaScript Array `filter()` method examples

由于filter()方法返回一个新数组，因此可以将结果数组与其他数组方法（例如sort()和map()）链接起来。

```js
let cities = [
  { name: 'Los Angeles', population: 3792621 },
  { name: 'New York', population: 8175133 },
  { name: 'Chicago', population: 2695598 },
  { name: 'Houston', population: 2099451 },
  { name: 'Philadelphia', population: 1526006 },
]
let res = cities
  .filter((city) => city.population < 3000000)
  .sort((c1, c2) => c1.population - c2.population)
  .map((city) => `${city.name}: ${city.population}`)
console.log(res) // [ 'Philadelphia: 1526006', 'Houston: 2099451', 'Chicago: 2695598' ]
```

以下示例说明了 `thisArg` 参数的用法，该参数指定可以使用 this 关键字在callback() 函数中引用的对象

```js
function isInRange(value) {
    if (typeof value !== 'number') {
        return false;
    }
    return value >= this.lower && value <= this.upper;
}
let data = [10, 20, "30", 1, 5, 'JavaScript filter', undefined, 'example'];
let range = {
    lower: 1,
    upper: 10
};
let numberInRange = data.filter(isInRange, range);
console.log(numberInRange); // [10, 1, 5]
```









