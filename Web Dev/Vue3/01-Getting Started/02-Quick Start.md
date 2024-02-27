# Quick Start

## Creating a Vue Application

Make sure you have an up-to-date version of Node.js installed and your current working directory is the one where you intend to create a project. Run the following command in your command line (without the `$` sign):

```sh
 npm create vue@latest
 // yarn create vue@latest
```

This command will install and execute create-vue, the official Vue project scaffolding tool. You will be presented with prompts for several optional features such as TypeScript and testing support:

```sh
✔ Project name: … <your-project-name>
✔ Add TypeScript? … No / Yes
✔ Add JSX Support? … No / Yes
✔ Add Vue Router for Single Page Application development? … No / Yes
✔ Add Pinia for state management? … No / Yes
✔ Add Vitest for Unit testing? … No / Yes
✔ Add an End-to-End Testing Solution? … No / Cypress / Playwright
✔ Add ESLint for code quality? … No / Yes
✔ Add Prettier for code formatting? … No / Yes

Scaffolding project in ./<your-project-name>...
Done.
```

If you are unsure about an option, simply choose `No` by hitting enter for now. Once the project is created, follow the instructions to install dependencies and start the dev server:

```sh
cd <your-project-name>
npm install
npm run dev
```

You should now have your first Vue project running! Note that the example components in the generated project are written using the Composition API and `<script setup>`, rather than the Options API. The recommended IDE setup is Visual Studio Code + Volar extension.

When you are ready to ship your app to production, run the following:

```sh
npm run build
```

This will create a production-ready build of your app in the project's `./dist` directory.

## Using Vue from CDN

You can use Vue directly from a CDN via a script tag:

```html
<script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>
```

When using Vue from a CDN, there is no "build step" involved. This makes the setup a lot simpler, and is suitable for enhancing static HTML or integrating with a backend framework. However, you won't be able to use the Single-File Component (SFC) syntax.

### Using the Global Build

The above link loads the *global build* of Vue, where all top-level APIs are exposed as properties on the global `Vue` object. Here is a full example using the global build:

```html
<script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>

<div id="app">{{ message }}</div>

<script>
  const { createApp } = Vue

  createApp({
    data() {
      return {
        message: 'Hello Vue!'
      }
    }
  }).mount('#app')
</script>
```

### Using the ES Module Build

Most modern browsers now support ES modules natively, so we can use Vue from a CDN via native ES modules like this:

```html
<div id="app">{{ message }}</div>

<script type="module">
  import { createApp } from 'https://unpkg.com/vue@3/dist/vue.esm-browser.js'

  createApp({
    data() {
      return {
        message: 'Hello Vue!'
      }
    }
  }).mount('#app')
</script>
```

Notice that we are using `<script type="module">`, and the imported CDN URL is pointing to the **ES modules build** of Vue instead.

### Enabling Import maps

In the above example, we are importing from the full CDN URL, but in the rest of the documentation you will see code like this:

```js
import { createApp } from 'vue'
```

We can teach the browser where to locate the `vue` import by using Import Maps:

```html
<script type="importmap">
  {
    "imports": {
      "vue": "https://unpkg.com/vue@3/dist/vue.esm-browser.js"
    }
  }
</script>

<div id="app">{{ message }}</div>

<script type="module">
  import { createApp } from 'vue'

  createApp({
    data() {
      return {
        message: 'Hello Vue!'
      }
    }
  }).mount('#app')
</script>
```

### Splitting Up the Modules

As we dive deeper into the guide, we may need to split our code into separate JavaScript files so that they are easier to manage. For example:

```html
<!-- index.html -->
<div id="app"></div>

<script type="module">
  import { createApp } from 'vue'
  import MyComponent from './my-component.js'

  createApp(MyComponent).mount('#app')
</script>
```

```js
// my-component.js
export default {
  data() {
    return { count: 0 }
  },
  template: `<div>count is {{ count }}</div>`
}
```

If you directly open the above `index.html` in your browser, you will find that it throws an error because ES modules cannot work over the `file://` protocol, which is the protocol the browser uses when you open a local file.

Due to security reasons, ES modules can only work over the `http://` protocol, which is what the browsers use when opening pages on the web.