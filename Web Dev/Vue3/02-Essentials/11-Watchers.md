# Watchers

## 基本示例

计算属性允许我们声明性地计算衍生值。然而在有些情况下，我们需要在状态变化时执行一些“副作用”：例如更改 DOM，或是根据异步操作的结果去修改另一处的状态。

在选项式 API 中，我们可以使用 `watch` 选项在每次响应式属性发生变化时触发一个函数。

```js
export default {
  data() {
    return {
      question: '',
      answer: 'Questions usually contain a question mark. ;-)',
      loading: false
    }
  },
  watch: {
    // 每当 question 改变时，这个函数就会执行
    question(newQuestion, oldQuestion) {
      if (newQuestion.includes('?')) {
        this.getAnswer()
      }
    }
  },
  methods: {
    async getAnswer() {
      this.loading = true
      this.answer = 'Thinking...'
      try {
        const res = await fetch('https://yesno.wtf/api')
        this.answer = (await res.json()).answer
      } catch (error) {
        this.answer = 'Error! Could not reach the API. ' + error
      } finally {
        this.loading = false
      }
    }
  }
}
```

```vue
<p>
  Ask a yes/no question:
  <input v-model="question" :disabled="loading" />
</p>
<p>{{ answer }}</p>
```

## Deep Watchers

`watch` 默认是浅层的：被侦听的属性，仅在被赋新值时，才会触发回调函数——而嵌套属性的变化不会触发。如果想侦听所有嵌套的变更，你需要深层侦听器：

```js
export default {
  watch: {
    someObject: {
      handler(newValue, oldValue) {
        // 注意：在嵌套的变更中，
        // 只要没有替换对象本身，
        // 那么这里的 `newValue` 和 `oldValue` 相同
      },
      deep: true
    }
  }
}
```

> 深度侦听需要遍历被侦听对象中的所有嵌套的属性，当用于大型数据结构时，开销很大。因此请只在必要时才使用它，并且要留意性能。

## Eager Watchers

`watch` 默认是懒执行的：仅当数据源变化时，才会执行回调。但在某些场景中，我们希望在创建侦听器时，立即执行一遍回调。举例来说，我们想请求一些初始数据，然后在相关状态更改时重新请求数据。

我们可以用一个对象来声明侦听器，这个对象有 `handler` 方法和 `immediate: true` 选项，这样便能强制回调函数立即执行：

```js
export default {
  // ...
  watch: {
    question: {
      handler(newQuestion) {
        // 在组件实例创建时会立即调用
      },
      // 强制立即执行回调
      immediate: true
    }
  }
  // ...
}
```

回调函数的初次执行就发生在 `created` 钩子之前。Vue 此时已经处理了 `data`、`computed` 和 `methods` 选项，所以这些属性在第一次调用时就是可用的。

## 一次性侦听器 

每当被侦听源发生变化时，侦听器的回调就会执行。如果希望回调只在源变化时触发一次，使用 `once: true` 选项。

## 回调的触发时机

当你更改了响应式状态，它可能会同时触发 Vue 组件更新和侦听器回调。

类似于组件更新，用户创建的侦听器回调函数也会被批量处理以避免重复调用。例如，如果我们同步将一千个项目推入被侦听的数组中，我们可能不希望侦听器触发一千次。

默认情况下，侦听器回调会在父组件更新 (如有) **之后**、所属组件的 DOM 更新**之前**被调用。这意味着如果你尝试在侦听器回调中访问所属组件的 DOM，那么 DOM 将处于更新前的状态。

### Post Watchers

如果想在侦听器回调中能访问被 Vue 更新**之后**的所属组件的 DOM，你需要指明 `flush: 'post'` 选项：

```js
export default {
  // ...
  watch: {
    key: {
      handler() {},
      flush: 'post'
    }
  }
}
```

### Sync Watchers

你还可以创建一个同步触发的侦听器，它会在 Vue 进行任何更新之前触发：

```js
export default {
  // ...
  watch: {
    key: {
      handler() {},
      flush: 'sync'
    }
  }
}
```

> 同步侦听器不会进行批处理，每当检测到响应式数据发生变化时就会触发。可以使用它来监视简单的布尔值，但应避免在可能多次同步修改的数据源 (如数组) 上使用。

## `this.$watch()`

也可以使用组件实例的 `$watch()` 方法来命令式地创建一个侦听器：

```js
export default {
  created() {
    this.$watch('question', (newQuestion) => {
      // ...
    })
  }
}
```

如果要在特定条件下设置一个侦听器，或者只侦听响应用户交互的内容，这方法很有用。它还允许你提前停止该侦听器。

## 停止侦听器

用 `watch` 选项或者 `$watch()` 实例方法声明的侦听器，会在宿主组件卸载时自动停止。因此，在大多数场景下，你无需关心怎么停止它。

在少数情况下，你的确需要在组件卸载之前就停止一个侦听器，这时可以调用 `$watch()` API 返回的函数：

```js
const unwatch = this.$watch('foo', callback)

// ...当该侦听器不再需要时
unwatch()
```