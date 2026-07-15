# Vue.js 3 Documentation

Vue.js is a progressive JavaScript framework for building user interfaces. It builds on standard HTML, CSS, and JavaScript to provide a declarative, component-based programming model for developing web applications of any complexity. Vue's core features include declarative rendering with a template syntax that extends HTML, and a reactivity system that automatically tracks JavaScript state changes and efficiently updates the DOM.

This documentation covers Vue 3, the latest major version of the framework. Vue can be used in multiple ways: enhancing static HTML without a build step, embedding as Web Components, building Single-Page Applications (SPAs), implementing Server-Side Rendering (SSR), or generating Static Sites (SSG). The framework supports two API styles - the Options API (class-based mental model) and the Composition API (function-based, more flexible for complex applications).

## Creating a Vue Application

The `createApp()` function creates a Vue application instance from a root component. The application is then mounted to a DOM element.

```javascript
import { createApp } from 'vue'
import App from './App.vue'

// Create and mount the application
const app = createApp(App)
app.mount('#app')

// With inline component
createApp({
  data() {
    return { message: 'Hello Vue!' }
  }
}).mount('#app')

// Pass props to root component
createApp(App, { username: 'admin' }).mount('#app')
```

## Application Configuration

Configure global application settings including error handlers, global properties, and component registration.

```javascript
import { createApp } from 'vue'
import App from './App.vue'

const app = createApp(App)

// Global error handler
app.config.errorHandler = (err, instance, info) => {
  console.error('Global error:', err)
  console.log('Component:', instance)
  console.log('Error info:', info)
}

// Global properties accessible in all components
app.config.globalProperties.$http = axios
app.config.globalProperties.$filters = {
  currency(value) {
    return '$' + value.toFixed(2)
  }
}

// Register global component
app.component('MyButton', {
  template: '<button class="my-btn"><slot/></button>'
})

// Install plugin
app.use(MyPlugin, { option1: true })

// Application-level provide
app.provide('theme', 'dark')

app.mount('#app')
```

## Reactive State with ref()

The `ref()` function creates a reactive reference that can hold any value. Access the value via the `.value` property in JavaScript; in templates, refs are automatically unwrapped.

```javascript
import { ref, watch } from 'vue'

// Create reactive refs
const count = ref(0)
const user = ref({ name: 'John', age: 30 })
const items = ref(['apple', 'banana'])

// Access and modify
console.log(count.value) // 0
count.value++
console.log(count.value) // 1

// Object refs are deeply reactive
user.value.age = 31
items.value.push('cherry')

// In a component
export default {
  setup() {
    const message = ref('Hello')

    function updateMessage() {
      message.value = 'Updated!'
    }

    return { message, updateMessage }
  }
}
```

## Reactive Objects with reactive()

The `reactive()` function returns a reactive proxy of an object. Unlike `ref()`, no `.value` is needed, but it only works with objects.

```javascript
import { reactive, toRefs } from 'vue'

// Create reactive object
const state = reactive({
  count: 0,
  user: { name: 'Alice' },
  items: []
})

// Direct property access and mutation
state.count++
state.user.name = 'Bob'
state.items.push('item1')

// Destructure while keeping reactivity
const { count, user } = toRefs(state)
console.log(count.value) // Access via .value after toRefs

// Nested reactivity
const nested = reactive({
  deep: {
    nested: {
      value: 'deep'
    }
  }
})
nested.deep.nested.value = 'changed' // Triggers reactivity
```

## Computed Properties

The `computed()` function creates a cached, reactive computed value that automatically updates when its dependencies change.

```javascript
import { ref, computed } from 'vue'

const firstName = ref('John')
const lastName = ref('Doe')

// Read-only computed
const fullName = computed(() => {
  return `${firstName.value} ${lastName.value}`
})
console.log(fullName.value) // 'John Doe'

// Writable computed
const fullNameWritable = computed({
  get() {
    return `${firstName.value} ${lastName.value}`
  },
  set(newValue) {
    const names = newValue.split(' ')
    firstName.value = names[0]
    lastName.value = names[1] || ''
  }
})
fullNameWritable.value = 'Jane Smith'
console.log(firstName.value) // 'Jane'

// Computed with complex logic
const items = ref([1, 2, 3, 4, 5])
const evenItems = computed(() => items.value.filter(n => n % 2 === 0))
const total = computed(() => items.value.reduce((sum, n) => sum + n, 0))
```

## Watchers with watch() and watchEffect()

Vue provides two ways to watch reactive state: `watch()` for watching specific sources, and `watchEffect()` for automatic dependency tracking.

```javascript
import { ref, reactive, watch, watchEffect } from 'vue'

const count = ref(0)
const state = reactive({ name: 'Vue', version: 3 })

// Watch a single ref
watch(count, (newValue, oldValue) => {
  console.log(`Count changed from ${oldValue} to ${newValue}`)
})

// Watch a getter function
watch(
  () => state.name,
  (newName, oldName) => {
    console.log(`Name: ${oldName} -> ${newName}`)
  }
)

// Watch multiple sources
watch([count, () => state.version], ([newCount, newVersion], [oldCount, oldVersion]) => {
  console.log(`Count: ${newCount}, Version: ${newVersion}`)
})

// Watch with options
watch(count, (val) => console.log(val), {
  immediate: true,  // Run immediately on creation
  deep: true,       // Deep watch objects
  once: true        // Run only once (3.4+)
})

// watchEffect - auto-tracks dependencies
const stop = watchEffect(() => {
  console.log(`Count is: ${count.value}`)
  console.log(`Name is: ${state.name}`)
})

// Stop watching
stop()

// Cleanup side effects
watchEffect((onCleanup) => {
  const controller = new AbortController()
  fetch('/api/data', { signal: controller.signal })
  onCleanup(() => controller.abort())
})
```

## Lifecycle Hooks

Composition API lifecycle hooks let you run code at specific stages of a component's lifecycle.

```javascript
import {
  ref,
  onMounted,
  onUpdated,
  onUnmounted,
  onBeforeMount,
  onBeforeUpdate,
  onBeforeUnmount,
  onErrorCaptured
} from 'vue'

export default {
  setup() {
    const element = ref(null)
    const data = ref(null)

    onBeforeMount(() => {
      console.log('Component will mount')
    })

    onMounted(() => {
      console.log('Component mounted')
      console.log('DOM element:', element.value)
      // Fetch data, setup third-party libraries
      fetchData().then(res => data.value = res)
    })

    onBeforeUpdate(() => {
      console.log('Component will update')
    })

    onUpdated(() => {
      console.log('Component updated')
    })

    onBeforeUnmount(() => {
      console.log('Component will unmount')
    })

    onUnmounted(() => {
      console.log('Component unmounted')
      // Cleanup: remove event listeners, cancel timers
    })

    onErrorCaptured((err, instance, info) => {
      console.error('Error captured:', err)
      return false // Prevent error propagation
    })

    return { element, data }
  }
}
```

## Single-File Components with script setup

The `<script setup>` syntax provides a more concise way to write Composition API components with less boilerplate.

```vue
<script setup>
import { ref, computed, onMounted } from 'vue'
import ChildComponent from './ChildComponent.vue'

// Props declaration
const props = defineProps({
  title: String,
  count: {
    type: Number,
    default: 0
  }
})

// Emits declaration
const emit = defineEmits(['update', 'delete'])

// Reactive state
const message = ref('Hello')
const doubled = computed(() => props.count * 2)

// Methods
function handleClick() {
  message.value = 'Clicked!'
  emit('update', message.value)
}

// Lifecycle
onMounted(() => {
  console.log('Component mounted with title:', props.title)
})

// Expose to parent via template refs
defineExpose({
  message,
  reset: () => { message.value = 'Hello' }
})
</script>

<template>
  <div>
    <h1>{{ title }}</h1>
    <p>{{ message }}</p>
    <p>Doubled: {{ doubled }}</p>
    <button @click="handleClick">Click me</button>
    <ChildComponent />
  </div>
</template>

<style scoped>
h1 { color: blue; }
</style>
```

## Props with TypeScript

Define component props using TypeScript for full type inference and validation.

```vue
<script setup lang="ts">
// Type-only props declaration
const props = defineProps<{
  title: string
  count?: number
  items: string[]
  user: {
    name: string
    email: string
  }
}>()

// With defaults (3.5+ syntax)
const { title, count = 0, items = [] } = defineProps<{
  title: string
  count?: number
  items?: string[]
}>()

// With defaults using withDefaults (3.4 and below)
interface Props {
  msg?: string
  labels?: string[]
}
const props2 = withDefaults(defineProps<Props>(), {
  msg: 'Hello',
  labels: () => ['one', 'two']
})

// Emits with types
const emit = defineEmits<{
  (e: 'change', id: number): void
  (e: 'update', value: string): void
}>()

// Or using named tuple syntax (3.3+)
const emit2 = defineEmits<{
  change: [id: number]
  update: [value: string]
}>()

emit('change', 123)
emit('update', 'new value')
</script>
```

## Two-Way Binding with v-model and defineModel

Create two-way data bindings on form inputs and custom components using `v-model` and the `defineModel` macro.

```vue
<!-- Parent component -->
<script setup>
import { ref } from 'vue'
import CustomInput from './CustomInput.vue'

const text = ref('')
const count = ref(0)
</script>

<template>
  <!-- Native form elements -->
  <input v-model="text" />
  <input v-model.lazy="text" />    <!-- Update on change -->
  <input v-model.number="count" /> <!-- Cast to number -->
  <input v-model.trim="text" />    <!-- Trim whitespace -->

  <!-- Custom component -->
  <CustomInput v-model="text" />
  <CustomInput v-model:title="text" v-model:count="count" />
</template>

<!-- CustomInput.vue -->
<script setup>
// Basic v-model (modelValue prop)
const model = defineModel()

// Named v-model
const title = defineModel('title')
const count = defineModel('count', { type: Number, default: 0 })

// With modifiers
const [modelValue, modifiers] = defineModel({
  set(value) {
    if (modifiers.capitalize) {
      return value.charAt(0).toUpperCase() + value.slice(1)
    }
    return value
  }
})
</script>

<template>
  <input :value="model" @input="model = $event.target.value" />
</template>
```

## Template Directives

Vue provides built-in directives for declarative DOM manipulation and event handling.

```vue
<template>
  <!-- Text interpolation -->
  <span>{{ message }}</span>
  <span v-text="message"></span>

  <!-- Raw HTML (use with caution) -->
  <div v-html="rawHtml"></div>

  <!-- Attribute binding -->
  <img :src="imageUrl" :alt="imageAlt" />
  <div :class="{ active: isActive, 'text-danger': hasError }"></div>
  <div :class="[activeClass, errorClass]"></div>
  <div :style="{ color: textColor, fontSize: size + 'px' }"></div>

  <!-- Conditional rendering -->
  <div v-if="type === 'A'">A</div>
  <div v-else-if="type === 'B'">B</div>
  <div v-else>Other</div>

  <!-- v-show (toggle display CSS) -->
  <div v-show="isVisible">Toggleable</div>

  <!-- List rendering -->
  <ul>
    <li v-for="item in items" :key="item.id">
      {{ item.name }}
    </li>
  </ul>
  <div v-for="(value, key, index) in object" :key="key">
    {{ index }}. {{ key }}: {{ value }}
  </div>

  <!-- Event handling -->
  <button @click="handleClick">Click</button>
  <button @click="count++">Increment</button>
  <button @click.prevent="submit">Submit</button>
  <button @click.stop="doThis">Stop propagation</button>
  <input @keyup.enter="onEnter" />
  <button @click.once="doOnce">Once only</button>

  <!-- Two-way binding -->
  <input v-model="text" />

  <!-- Slots -->
  <BaseLayout>
    <template #header>Header content</template>
    <template #default>Main content</template>
    <template #footer>Footer content</template>
  </BaseLayout>

  <!-- Performance optimization -->
  <span v-once>{{ staticContent }}</span>
  <div v-memo="[valueA, valueB]">Memoized</div>
</template>
```

## Provide and Inject

Pass data through the component tree without prop drilling using the provide/inject pattern.

```javascript
// Parent component providing values
import { ref, provide, readonly } from 'vue'

export default {
  setup() {
    const theme = ref('dark')
    const user = ref({ name: 'John' })

    // Provide reactive values
    provide('theme', theme)

    // Provide readonly to prevent child mutations
    provide('user', readonly(user))

    // Provide methods
    provide('updateTheme', (newTheme) => {
      theme.value = newTheme
    })

    return { theme, user }
  }
}

// Child/descendant component injecting values
import { inject } from 'vue'

export default {
  setup() {
    // Inject with default value
    const theme = inject('theme', 'light')
    const user = inject('user')
    const updateTheme = inject('updateTheme')

    // Inject with factory function for default
    const config = inject('config', () => ({ debug: false }), true)

    return { theme, user, updateTheme }
  }
}

// App-level provide
const app = createApp(App)
app.provide('globalConfig', { apiUrl: '/api' })
```

## Composables

Composables are reusable functions that encapsulate stateful logic using the Composition API.

```javascript
// useMouse.js - Track mouse position
import { ref, onMounted, onUnmounted } from 'vue'

export function useMouse() {
  const x = ref(0)
  const y = ref(0)

  function update(event) {
    x.value = event.pageX
    y.value = event.pageY
  }

  onMounted(() => window.addEventListener('mousemove', update))
  onUnmounted(() => window.removeEventListener('mousemove', update))

  return { x, y }
}

// useFetch.js - Async data fetching
import { ref, watchEffect, toValue } from 'vue'

export function useFetch(url) {
  const data = ref(null)
  const error = ref(null)
  const isLoading = ref(false)

  async function fetchData() {
    isLoading.value = true
    error.value = null

    try {
      const response = await fetch(toValue(url))
      if (!response.ok) throw new Error('Network error')
      data.value = await response.json()
    } catch (e) {
      error.value = e
    } finally {
      isLoading.value = false
    }
  }

  watchEffect(() => {
    fetchData()
  })

  return { data, error, isLoading, refetch: fetchData }
}

// Usage in component
import { useMouse } from './useMouse'
import { useFetch } from './useFetch'

export default {
  setup() {
    const { x, y } = useMouse()
    const { data, error, isLoading } = useFetch('/api/users')

    return { x, y, data, error, isLoading }
  }
}
```

## Custom Directives

Create custom directives to encapsulate reusable DOM manipulation logic.

```javascript
// Global directive registration
app.directive('focus', {
  mounted(el) {
    el.focus()
  }
})

// Directive with all hooks
app.directive('highlight', {
  created(el, binding, vnode, prevVnode) {},
  beforeMount(el, binding) {},
  mounted(el, binding) {
    el.style.backgroundColor = binding.value || 'yellow'
  },
  beforeUpdate(el, binding) {},
  updated(el, binding) {
    el.style.backgroundColor = binding.value || 'yellow'
  },
  beforeUnmount(el) {},
  unmounted(el) {}
})

// Function shorthand (mounted + updated)
app.directive('color', (el, binding) => {
  el.style.color = binding.value
})

// Local directive in script setup
const vClickOutside = {
  mounted(el, binding) {
    el._clickOutside = (event) => {
      if (!el.contains(event.target)) {
        binding.value(event)
      }
    }
    document.addEventListener('click', el._clickOutside)
  },
  unmounted(el) {
    document.removeEventListener('click', el._clickOutside)
  }
}

// Usage in template
// <input v-focus />
// <div v-highlight="'lightblue'">Highlighted</div>
// <div v-click-outside="handleClickOutside">Dropdown</div>
```

## Plugins

Create plugins to add app-level functionality, including global components, directives, and instance properties.

```javascript
// myPlugin.js
export default {
  install(app, options) {
    // Add global method
    app.config.globalProperties.$translate = (key) => {
      return options.translations[key] || key
    }

    // Add global component
    app.component('MyGlobalComponent', {
      template: '<div>Global Component</div>'
    })

    // Add global directive
    app.directive('my-directive', {
      mounted(el) {
        // ...
      }
    })

    // Provide something injectable
    app.provide('pluginOptions', options)

    // Add instance method
    app.config.globalProperties.$doSomething = function() {
      // Access component instance via `this`
    }
  }
}

// main.js - Using the plugin
import { createApp } from 'vue'
import MyPlugin from './myPlugin'
import App from './App.vue'

const app = createApp(App)
app.use(MyPlugin, {
  translations: {
    hello: 'Bonjour',
    goodbye: 'Au revoir'
  }
})
app.mount('#app')
```

## CDN Usage Without Build Tools

Use Vue directly in HTML via CDN for simple projects or progressive enhancement.

```html
<!DOCTYPE html>
<html>
<head>
  <title>Vue CDN Example</title>
</head>
<body>
  <div id="app">
    <h1>{{ message }}</h1>
    <button @click="count++">Count: {{ count }}</button>
    <ul>
      <li v-for="item in items" :key="item">{{ item }}</li>
    </ul>
  </div>

  <!-- Using ES modules -->
  <script type="importmap">
    {
      "imports": {
        "vue": "https://unpkg.com/vue@3/dist/vue.esm-browser.js"
      }
    }
  </script>

  <script type="module">
    import { createApp, ref, computed } from 'vue'

    createApp({
      setup() {
        const message = ref('Hello Vue!')
        const count = ref(0)
        const items = ref(['Apple', 'Banana', 'Cherry'])

        return { message, count, items }
      }
    }).mount('#app')
  </script>
</body>
</html>
```

## Summary

Vue.js 3 provides a comprehensive framework for building modern web applications. The Composition API enables better code organization and reuse through composables, while Single-File Components (SFCs) with `<script setup>` offer a clean, concise syntax for component development. Key use cases include building SPAs with Vue Router and Pinia for state management, creating reusable component libraries, progressive enhancement of existing applications, and server-side rendering for improved SEO and initial load performance.

The framework integrates seamlessly with TypeScript for type-safe development, and its reactive system based on `ref()`, `reactive()`, `computed()`, and `watch()` provides predictable state management. Vue's template directives (`v-if`, `v-for`, `v-model`, `v-on`, `v-bind`) enable declarative DOM manipulation, while the provide/inject system and composables facilitate clean dependency injection and logic reuse across component hierarchies. For projects requiring build tools, Vite is the recommended choice, while CDN-based usage remains fully supported for simpler use cases.
