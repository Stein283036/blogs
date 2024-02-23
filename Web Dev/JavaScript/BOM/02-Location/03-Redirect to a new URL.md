# JavaScript Redirect

## Introduction to the JavaScript redirect

The redirection can be done in the web browsers using JavaScript redirection API.

It’s important to note that JavaScript redirection runs entirely on web browsers. Therefore it doesn’t return the status code 301 (move permanently) like a server redirection.

Therefore, if you move the site to a separate domain or create a new URL for an old page, you should always use the server redirection.

## Redirect to a new URL

To redirect web browsers to a new URL from the current page to a new one, you use the `location` object:

```js
location.href = 'new_url';
```

```js
location.href = 'https://www.javascripttutorial.net/';
```

Assigning a value to the `href` property of the `location` object has the same effect as calling the `assign()` method of the `location` object:

```js
location.assign('https://www.javascripttutorial.net/');
```

这些调用中的任何一个都会重定向到新的 URL 并在浏览器的历史堆栈中创建一个条目。这意味着可以通过浏览器的后退按钮返回到上一页。

## Redirect to a relative URL

The following script redirects to the `about.html` which is on the same level as the current page.

```js
location.href = 'about.html';
```

The following script redirects to `contact.html` page located in the `root` folder:

```js
location.href = '/contact.html';
```

## Redirect upon page loading

```js
window.onload = function() {
    location.href = "https://www.javascripttutorial.net/";
}
```