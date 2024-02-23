# JavaScript prompt

## Introduction to JavaScript `prompt()` method

The `prompt()` is a method of the `window` object. The `prompt()` method instructs the web browser to display a dialog with a text, text input field, and two buttons `OK` and `Cancel`.

The dialog prompts the user to enter some text and wait until the user either submits or cancels it.

```js
let result = window.prompt(message, default);
```

In this syntax:

- The `message` is a string to display. If you omit it, nothing will display on the dialog.
- The `default` is a string containing the default value of the text input field.

The result is a string that contains the text entered by the user or `null`.

Like `alert()` and `confirm()`, the `prompt()` is modal and synchronous. In other words, the code execution stops when the dialog is displayed and resumes after the dialog has been dismissed.

## JavaScript `prompt()` examples

### Display a prompt dialog

```js
let lang = prompt('What is your favorite programming language?');
let feedback = lang.toLowerCase() === 'javascript' ? `It's great!` :
    `It's ${lang}`;
alert(feedback);
```

### Convert a user input to a number

The result of the `prompt()` is a string. If you want to get the answer as a number, you should always cast the string into a number.

```js
let ageStr = prompt('How old are you?');
let age = Number(ageStr);
let feedback = age >= 16 ?
    "You're eligible to join." :
    'You must be at least 16 year old to join.';
alert(feedback);
```