# if-else if-else

## if

The `if` statement executes block if a condition is `true`. The following shows the syntax of the `if` statement:

```js
if( condition ) {
    statement;   
}
```

The condition can be a value or an expression. Typically, the condition evaluates to a Boolean value, which is true or false.

If the condition evaluates to a non-Boolean value, JavaScript implicitly converts its result to a Boolean value by calling the Boolean() function.

It’s possible to use an `if` statement inside another `if` statement.

```js
let age = 16;
let state = 'CA';

if (state == 'CA') {
  if (age >= 16) {
    console.log('You can drive.');
  }
}
```

In practice, you should avoid using nested `if` statements as much as possible. For example, you can use the `&&` operator to combine the conditions and use an `if` statements as follows:

```js
let age = 16;
let state = 'CA';

if (state == 'CA' && age == 16) {
  console.log('You can drive.');
}
```

## if-else

The following shows the syntax of the `if...else` statement:

```js
if( condition ) {
  // ...
} else { 
  // ...
}
```

## if-else if

```js
if (condition1) {
  // ...
} else if (condition2) {
  // ...
} else if (condition3) {
  //...
} else {
  //...
}
```









