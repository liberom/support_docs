### Start Vue 3 Migration Guide Development Server

Source: https://github.com/vuejs/v3-migration-guide/blob/main/README.md

This command initiates the local development server for the Vue 3 migration guide documentation. It allows developers to preview changes in real-time while working on the documentation.

```Shell
pnpm dev
```

--------------------------------

### Vue SFC Script Setup Component Import

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/index.md

An example of importing a component using the `<script setup>` syntax within a Vue Single File Component (SFC). This syntax simplifies component setup by allowing top-level imports and variable declarations to be directly exposed to the template.

```Vue
<script setup>
import VueMasteryWidget from './VueMastery.vue'
</script>
```

--------------------------------

### Vue 2.x Event Bus Implementation Example

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/breaking-changes/events-api.md

Demonstrates how a global event bus was typically implemented in Vue 2.x using a Vue instance. It shows the setup of the event bus, how a child component would listen for custom events, and how a parent component would emit those events.

```javascript
// eventBus.js

const eventBus = new Vue()

export default eventBus
```

```javascript
// ChildComponent.vue
import eventBus from './eventBus'

export default {
  mounted() {
    // adding eventBus listener
    eventBus.$on('custom-event', () => {
      console.log('Custom event triggered!')
    })
  },
  beforeDestroy() {
    // removing eventBus listener
    eventBus.$off('custom-event')
  }
}
```

```javascript
// ParentComponent.vue
import eventBus from './eventBus'

export default {
  methods: {
    callGlobalCustomEvent() {
      eventBus.$emit('custom-event') // if ChildComponent is mounted, we will have a message in the console
    }
  }
}
```

--------------------------------

### Vue 3 Migration: GLOBAL_MOUNT

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/migration-build.md

The global `new Vue()` API has been replaced by `createApp` for mounting application instances. This change promotes better tree-shaking and a more explicit application setup.

```APIDOC
Change ID: GLOBAL_MOUNT
Description: `new Vue()` is replaced by `createApp` for mounting app instances.
Old API: `new Vue(options)`
New API: `createApp(rootComponent, rootProps)`
```

--------------------------------

### Build Vue 3 Migration Guide Documentation

Source: https://github.com/vuejs/v3-migration-guide/blob/main/README.md

This command compiles the Vue 3 migration guide documentation into static files. The output is ready for deployment to a web server.

```Shell
pnpm build
```

--------------------------------

### Serve Built Vue 3 Migration Guide Documentation

Source: https://github.com/vuejs/v3-migration-guide/blob/main/README.md

This command serves the previously built static documentation files locally. It is useful for testing the production build of the documentation before actual deployment.

```Shell
pnpm serve
```

--------------------------------

### Vue SFC Style Block Example

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/index.md

A CSS style block demonstrating how to define styles within a Vue Single File Component (SFC). This specific example defines a color for elements with the 'note' class.

```CSS
<style>
.note {
  color: #476582;
}
</style>
```

--------------------------------

### Vue 2 Plugin: Global API Usage Example

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/breaking-changes/global-api-treeshaking.md

Illustrates a Vue 2.x plugin's `install` method accessing a global API, such as `Vue.nextTick`, directly from the `Vue` instance passed as an argument.

```javascript
const plugin = {
  install: Vue => {
    Vue.nextTick(() => {
      // ...
    })
  }
}
```

--------------------------------

### Vue 2 Plugin Installation with Vue.use (UMD)

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/breaking-changes/global-api.md

Illustrates the common practice in Vue 2 for plugin authors to automatically install plugins in UMD builds using the global `Vue.use` API, typically checking for a browser environment before installation.

```js
var inBrowser = typeof window !== 'undefined'
/* … */
if (inBrowser && window.Vue) {
  window.Vue.use(VueRouter)
}
```

--------------------------------

### Vue 3 Plugin Installation with App Instance

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/breaking-changes/global-api.md

Demonstrates the new method for installing plugins in Vue 3, where the end-user explicitly calls `app.use()` on an app instance, replacing the deprecated global `Vue.use` API.

```js
const app = createApp(MyApp)
app.use(VueRouter)
```

--------------------------------

### Compare Vue 3 Migration Guide Translations

Source: https://github.com/vuejs/v3-migration-guide/blob/main/README.md

This command compares the current state of the documentation translations with the latest checkpoint for a specified language. It helps identify any discrepancies or outdated translations.

```Shell
pnpm translation:compare <lang>
```

--------------------------------

### Vue 3.x Template Compilation Example: Transition with v-show

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/breaking-changes/global-api-treeshaking.md

An example of a Vue 3.x template using <transition> and v-show, illustrating how the compiler processes it to import only necessary components and directives, which is crucial for tree-shaking.

```html
<transition>
  <div v-show="ok">hello</div>
</transition>
```

--------------------------------

### Configure Build Tools for Vue 3 Compatibility Mode

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/migration-build.md

These code examples demonstrate how to configure different build tools (Vue CLI, plain webpack, and Vite) to alias 'vue' to '@vue/compat' and enable Vue 3 compatibility mode (MODE: 2) in their respective Vue loader/plugin options.

```js
// vue.config.js
module.exports = {
  chainWebpack: (config) => {
    config.resolve.alias.set('vue', '@vue/compat')

    config.module
      .rule('vue')
      .use('vue-loader')
      .tap((options) => {
        return {
          ...options,
          compilerOptions: {
            compatConfig: {
              MODE: 2
            }
          }
        }
      })
  }
}
```

```js
// webpack.config.js
module.exports = {
  resolve: {
    alias: {
      vue: '@vue/compat'
    }
  },
  module: {
    rules: [
      {
        test: /\.vue$/,
        loader: 'vue-loader',
        options: {
          compilerOptions: {
            compatConfig: {
              MODE: 2
            }
          }
        }
      }
    ]
  }
}
```

```js
// vite.config.js
export default {
  resolve: {
    alias: {
      vue: '@vue/compat'
    }
  },
  plugins: [
    vue({
      template: {
        compilerOptions: {
          compatConfig: {
            MODE: 2
          }
        }
      }
    })
  ]
}
```

--------------------------------

### Vue 3 Migration: CONFIG_PRODUCTION_TIP

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/migration-build.md

`config.productionTip` no longer necessary

```APIDOC
ID: CONFIG_PRODUCTION_TIP
Type: ◐
Removed: config.productionTip (no longer necessary)
```

--------------------------------

### Vue 3 Plugin: Explicit API Import Example

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/breaking-changes/global-api-treeshaking.md

Shows the updated approach for Vue 3 plugins, where global APIs like `nextTick` are explicitly imported from the 'vue' module, and the `install` method receives the `app` instance.

```javascript
import { nextTick } from 'vue'

const plugin = {
  install: app => {
    nextTick(() => {
      // ...
    })
  }
}
```

--------------------------------

### Vue 3 Custom Directive Definition and Usage

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/breaking-changes/custom-directives.md

Shows how to define and apply a custom directive in Vue 3 using the `beforeMount` hook. This example mirrors the Vue 2 functionality for setting an element's background style.

```html
<p v-highlight="'yellow'">Highlight this text bright yellow</p>
```

```javascript
const app = Vue.createApp({})

app.directive('highlight', {
  beforeMount(el, binding, vnode) {
    el.style.background = binding.value
  }
})
```

--------------------------------

### Vue 3 Migration: OPTIONS_BEFORE_DESTROY

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/migration-build.md

The lifecycle hook `beforeDestroy` has been renamed to `beforeUnmount` in Vue 3 for clearer semantics.

```APIDOC
Change ID: OPTIONS_BEFORE_DESTROY
Description: `beforeDestroy` has been renamed to `beforeUnmount`.
Old Hook: `beforeDestroy()`
New Hook: `beforeUnmount()`
```

--------------------------------

### Vue 3 Migration: CONFIG_IGNORED_ELEMENTS

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/migration-build.md

`config.ignoredElements` is now `config.compilerOptions.isCustomElement` (only in browser compiler build). If using build setup, `isCustomElement` must be passed via build configuration.

```APIDOC
ID: CONFIG_IGNORED_ELEMENTS
Type: ◐
Old API: config.ignoredElements
New API: config.compilerOptions.isCustomElement
Notes: Only in browser compiler build. If using build setup, isCustomElement must be passed via build configuration.
```

--------------------------------

### Show Vue 3 Migration Guide Translation Status

Source: https://github.com/vuejs/v3-migration-guide/blob/main/README.md

This command displays the current translation status for the documentation. Users can optionally specify a language code (e.g., 'zh', 'ja') to view the status for a particular language; otherwise, it provides an overview for all available languages.

```Shell
pnpm translation:status [<lang>]
```

--------------------------------

### Vue 3 Migration: TRANSITION_CLASSES

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/migration-build.md

Transition enter/leave classes changed

```APIDOC
ID: TRANSITION_CLASSES
Type: ⭘
Change: Transition enter/leave classes changed
```

--------------------------------

### Vue 3 Migration: INSTANCE_SET

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/migration-build.md

The instance method `vm.$set` has been removed in Vue 3. It is no longer necessary due to Vue 3's improved reactivity system.

```APIDOC
Change ID: INSTANCE_SET
Description: `vm.$set` has been removed.
Reason: No longer needed due to Vue 3's reactivity system.
```

--------------------------------

### Scaffold New Vue 3 Project with Vite

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/recommendations.md

This command uses `create-vue` to initialize a new Vue 3 project, which is powered by Vite. Vite is the recommended build toolchain for new Vue 3 applications, offering extremely fast server start and hot update performance.

```sh
npm init vue@3
```

--------------------------------

### Vue 3 Migration: GLOBAL_PRIVATE_UTIL

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/migration-build.md

`Vue.util` is private and no longer available

```APIDOC
ID: GLOBAL_PRIVATE_UTIL
Type: ◐
Removed: Vue.util (private utility)
```

--------------------------------

### Vue 3 Migration: COMPILER_INLINE_TEMPLATE

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/migration-build.md

`inline-template` removed (compat only supported in browser compiler build)

```APIDOC
ID: COMPILER_INLINE_TEMPLATE
Type: ◐
Removed: inline-template attribute
Notes: Compat only supported in browser compiler build.
```

--------------------------------

### Vue.js Incompatible Features Reference

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/migration-build.md

Lists features that are incompatible between Vue 2 and Vue 3, requiring upfront fixes or likely leading to errors during migration.

```APIDOC
Incompatible Features:
  - ID: GLOBAL_MOUNT_CONTAINER
    Type: ⨂
    Description: Mounted application does not replace the element it's mounted to
    Docs: ./breaking-changes/mount-changes.html
  - ID: CONFIG_DEVTOOLS
    Type: ⨂
    Description: production devtools is now a build-time flag
    Docs: https://github.com/vuejs/core/tree/master/packages/vue#bundler-build-feature-flags
  - ID: COMPILER_V_IF_V_FOR_PRECEDENCE
    Type: ⨂
    Description: `v-if` and `v-for` precedence when used on the same element has changed
    Docs: ./breaking-changes/v-if-v-for.html
  - ID: COMPILER_V_IF_SAME_KEY
    Type: ⨂
    Description: `v-if` branches can no longer have the same key
    Docs: ./breaking-changes/key-attribute.html#on-conditional-branches
  - ID: COMPILER_V_FOR_TEMPLATE_KEY_PLACEMENT
    Type: ⨂
    Description: `<template v-for>` key should now be placed on `<template>`
    Docs: ./breaking-changes/key-attribute.html#with-template-v-for
  - ID: COMPILER_SFC_FUNCTIONAL
    Type: ⨂
    Description: `<template functional>` is no longer supported in SFCs
    Docs: ./breaking-changes/functional-components.html#single-file-components-sfcs
```

--------------------------------

### Vue 3 Migration: CONFIG_KEY_CODES

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/migration-build.md

The `config.keyCodes` option has been removed in Vue 3. Key code modifiers for `v-on` are no longer supported.

```APIDOC
Change ID: CONFIG_KEY_CODES
Description: `config.keyCodes` has been removed.
Reason: Key code modifiers are no longer supported.
```

--------------------------------

### Vue 3 Migration: INSTANCE_DESTROY

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/migration-build.md

`$destroy` instance method removed (in compat mode, only supported on root instance)

```APIDOC
ID: INSTANCE_DESTROY
Type: ◐
Removed: $destroy instance method
Notes: In compat mode, only supported on root instance.
```

--------------------------------

### Vue.js Compatibility Feature Types Reference

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/migration-build.md

Defines the symbols used to indicate the compatibility status of features during Vue 3 migration.

```APIDOC
Compatibility Types:
- ✔ Fully compatible
- ◐ Partially Compatible with caveats
- ⨂ Incompatible (warning only)
- ⭘ Compat only (no warning)
```

--------------------------------

### Update Vue 3 Migration Guide Translation Checkpoint

Source: https://github.com/vuejs/v3-migration-guide/blob/main/README.md

This command updates the translation checkpoint for a specified language. By default, the checkpoint is set to the latest commit hash, but a specific commit hash can also be provided manually to define the checkpoint.

```Shell
pnpm translation:update <lang> [<commit>]
```

--------------------------------

### Update Vue and Compat Dependencies in package.json

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/migration-build.md

This diff snippet illustrates the required modifications in `package.json` to upgrade Vue to version 3.1, introduce `@vue/compat` for backward compatibility, and replace `vue-template-compiler` with `@vue/compiler-sfc`.

```diff
"dependencies": {
-  "vue": "^2.6.12",
+  "vue": "^3.1.0",
+  "@vue/compat": "^3.1.0"
   ...
},
"devDependencies": {
-  "vue-template-compiler": "^2.6.12"
+  "@vue/compiler-sfc": "^3.1.0"
}
```

--------------------------------

### Vue 3 Migration: CONFIG_SILENT

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/migration-build.md

`config.silent` removed

```APIDOC
ID: CONFIG_SILENT
Type: ◐
Removed: config.silent
```

--------------------------------

### Configure Per-Component Vue Compat Options

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/migration-build.md

Illustrates how to apply compatibility configurations on a per-component basis using the `compatConfig` option, allowing individual components to opt into Vue 3 behavior or toggle specific features.

```js
export default {
  compatConfig: {
    MODE: 3, // opt-in to Vue 3 behavior for this component only
    FEATURE_ID_A: true // features can also be toggled at component level
  }
  // ...
}
```

--------------------------------

### Vue 3 Migration: INSTANCE_EVENT_HOOKS

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/migration-build.md

Component instances in Vue 3 no longer emit `hook:x` events. Lifecycle hooks are now directly available as options.

```APIDOC
Change ID: INSTANCE_EVENT_HOOKS
Description: Instance no longer emits `hook:x` events.
```

--------------------------------

### Vue 2.x v-bind.sync for Two-Way Binding

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/breaking-changes/v-model.md

Explains the `update:myPropName` event pattern for two-way binding in Vue 2.x and the `.sync` modifier as a convenient shorthand for this pattern.

```javascript
this.$emit('update:title', newValue)
```

```html
<ChildComponent :title="pageTitle" @update:title="pageTitle = $event" />
```

```html
<ChildComponent :title.sync="pageTitle" />
```

--------------------------------

### Vue 3 Migration: OPTIONS_DESTROYED

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/migration-build.md

The lifecycle hook `destroyed` has been renamed to `unmounted` in Vue 3 for clearer semantics.

```APIDOC
Change ID: OPTIONS_DESTROYED
Description: `destroyed` has been renamed to `unmounted`.
Old Hook: `destroyed()`
New Hook: `unmounted()`
```

--------------------------------

### Vue 3 Migration: INSTANCE_LISTENERS

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/migration-build.md

The instance property `vm.$listeners` has been removed in Vue 3. Listeners are now part of `vm.$attrs`.

```APIDOC
Change ID: INSTANCE_LISTENERS
Description: `vm.$listeners` has been removed.
Reason: Listeners are now included in `vm.$attrs`.
```

--------------------------------

### Vue 3 Migration: INSTANCE_EVENT_EMITTER

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/migration-build.md

The instance event emitter methods `vm.$on`, `vm.$off`, and `vm.$once` have been removed from the component instance in Vue 3. Event bus patterns should now use a dedicated external library.

```APIDOC
Change ID: INSTANCE_EVENT_EMITTER
Description: `vm.$on`, `vm.$off`, `vm.$once` have been removed from component instances.
Recommendation: Use an external event library or provide/inject for component communication.
```

--------------------------------

### Vue 3 Migration: GLOBAL_PROTOTYPE

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/migration-build.md

The `Vue.prototype` property has been replaced by `app.config.globalProperties` for defining global properties accessible across all components.

```APIDOC
Change ID: GLOBAL_PROTOTYPE
Description: `Vue.prototype` is replaced by `app.config.globalProperties`.
Old API: `Vue.prototype.myProperty = value`
New API: `app.config.globalProperties.myProperty = value`
```

--------------------------------

### Vue 3 Migration: GLOBAL_EXTEND

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/migration-build.md

The global `Vue.extend` method has been removed in Vue 3. Developers should now use `defineComponent` or the `extends` option for component definition and extension.

```APIDOC
Change ID: GLOBAL_EXTEND
Description: `Vue.extend` has been removed.
Recommendation: Use `defineComponent` or the `extends` option instead.
```

--------------------------------

### Configure Global Vue Compat: Default to Vue 3, Enable Specific Features

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/migration-build.md

Shows how to configure the entire application to default to Vue 3 behavior while selectively enabling specific compatibility features using `configureCompat`.

```js
import { configureCompat } from 'vue'

// default everything to Vue 3 behavior, and only enable compat
// for certain features
configureCompat({
  MODE: 3,
  FEATURE_ID_A: true,
  FEATURE_ID_B: true
})
```

--------------------------------

### Vue 3 Migration: CONFIG_WHITESPACE

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/migration-build.md

In Vue 3, the default whitespace handling for templates has changed to `"condense"`.

```APIDOC
Change ID: CONFIG_WHITESPACE
Description: In Vue 3, whitespace defaults to `"condense"`.
```

--------------------------------

### Vue 3.x v-model Arguments for Custom Props

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/breaking-changes/v-model.md

Demonstrates how Vue 3.x replaces the `model` option and `.sync` modifier with `v-model` arguments to specify custom prop names for two-way binding, enhancing flexibility.

```html
<ChildComponent v-model:title="pageTitle" />

<!-- would be shorthand for: -->

<ChildComponent :title="pageTitle" @update:title="pageTitle = $event" />
```

--------------------------------

### Vue 3 Migration: OPTIONS_DATA_MERGE

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/migration-build.md

When using mixins or extensions, `data` from mixins is now shallow merged into the component's data.

```APIDOC
Change ID: OPTIONS_DATA_MERGE
Description: `data` from mixin or extension is now shallow merged.
```

--------------------------------

### Vue 3 Migration: OPTIONS_DATA_FN

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/migration-build.md

In Vue 3, the `data` option must always be a function, even for root instances. This ensures proper data isolation and reactivity.

```APIDOC
Change ID: OPTIONS_DATA_FN
Description: `data` must be a function in all cases.
Old: `data: { message: 'hi' }` (for root instance)
New: `data() { return { message: 'hi' } }` (always)
```

--------------------------------

### Vue 2 Global APIs vs. Vue 3 Instance APIs Migration Guide

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/breaking-changes/global-api.md

A mapping table showing the migration path for global APIs from Vue 2 to their corresponding instance-level APIs in Vue 3. This highlights how global mutations are now scoped to specific app instances, improving modularity and testability.

```APIDOC
Vue 2.x Global API | 3.x Instance API (app)
-------------------|-----------------------
Vue.config         | app.config
Vue.config.productionTip | _removed_
Vue.config.ignoredElements | app.config.compilerOptions.isCustomElement
Vue.component      | app.component
Vue.directive      | app.directive
Vue.mixin          | app.mixin
Vue.use            | app.use
Vue.prototype      | app.config.globalProperties
Vue.extend         | _removed_
```

--------------------------------

### Update Vue 2 v-model Prop and Event Names for Vue 3

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/breaking-changes/v-model.md

When migrating `v-model` without arguments from Vue 2 to Vue 3, the default prop name changes from `value` to `modelValue` and the default event name changes from `input` to `update:modelValue`. This example shows the necessary updates in both the parent component's template and the child component's script.

```html
<ChildComponent v-model="pageTitle" />
```

```javascript
// ChildComponent.vue

export default {
  props: {
    modelValue: String // previously was `value: String`
  },
  emits: ['update:modelValue'],
  methods: {
    changePageTitle(title) {
      this.$emit('update:modelValue', title) // previously was `this.$emit('input', title)`
    }
  }
}
```

--------------------------------

### Vue 3 Migration: GLOBAL_OBSERVABLE

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/migration-build.md

The global `Vue.observable` method has been removed in Vue 3. Its functionality is now covered by the `reactive` API from the reactivity core.

```APIDOC
Change ID: GLOBAL_OBSERVABLE
Description: `Vue.observable` has been removed.
Recommendation: Use `reactive` from `vue` instead.
```

--------------------------------

### Vue 3: Example of $attrs object with ID and event listener

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/breaking-changes/listeners-removed.md

Provides a concrete example of the `$attrs` object's content in Vue 3, showing how both standard HTML attributes (like `id`) and event listeners (like `onClose`) are now part of the same object.

```js
{
  id: 'my-input',
  onClose: () => console.log('close Event triggered')
}
```

--------------------------------

### Configure Global Vue Compat: Disable Specific Features

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/migration-build.md

Demonstrates how to globally disable specific compatibility features in Vue 3 using `configureCompat` to opt out of Vue 2 behaviors.

```js
import { configureCompat } from 'vue'

// disable compat for certain features
configureCompat({
  FEATURE_ID_A: false,
  FEATURE_ID_B: false
})
```

--------------------------------

### Vue 3 Migration: PROPS_DEFAULT_THIS

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/migration-build.md

props default factory no longer have access to `this` (in compat mode, `this` is not a real instance - it only exposes props, `$options` and injections)

```APIDOC
ID: PROPS_DEFAULT_THIS
Type: ◐
Change: Props default factory no longer has access to `this`
Notes: In compat mode, `this` is not a real instance; it only exposes props, `$options`, and injections.
```

--------------------------------

### Vue 3 Migration: INSTANCE_DELETE

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/migration-build.md

The instance method `vm.$delete` has been removed in Vue 3. It is no longer necessary as Vue 3's reactivity system handles property deletions automatically.

```APIDOC
Change ID: INSTANCE_DELETE
Description: `vm.$delete` has been removed.
Reason: No longer needed due to Vue 3's reactivity system.
```

--------------------------------

### Vue 3 Migration: INSTANCE_CHILDREN

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/migration-build.md

The instance property `vm.$children` has been removed in Vue 3. Accessing child components directly is generally discouraged; use refs or provide/inject for communication.

```APIDOC
Change ID: INSTANCE_CHILDREN
Description: `vm.$children` has been removed.
Recommendation: Use `ref` for direct child access or provide/inject for communication.
```

--------------------------------

### Vue 3.x Multiple v-model Bindings on Components

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/breaking-changes/v-model.md

Illustrates the new capability in Vue 3.x to use multiple `v-model` directives on the same custom component, each targeting a different property via arguments.

```html
<ChildComponent v-model:title="pageTitle" v-model:content="pageContent" />

<!-- would be shorthand for: -->

<ChildComponent
  :title="pageTitle"
  @update:title="pageTitle = $event"
  :content="pageContent"
  @update:content="pageContent = $event"
/>
```

--------------------------------

### Vue 3 Migration: INSTANCE_ATTRS_CLASS_STYLE

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/migration-build.md

In Vue 3, the `$attrs` property now includes `class` and `style` attributes, providing a more comprehensive collection of non-prop attributes.

```APIDOC
Change ID: INSTANCE_ATTRS_CLASS_STYLE
Description: `$attrs` now includes `class` and `style` attributes.
```

--------------------------------

### Vue 3 Migration: V_ON_KEYCODE_MODIFIER

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/migration-build.md

The `v-on` directive in Vue 3 no longer supports keyCode modifiers. Event handling should rely on event.key or event.code.

```APIDOC
Change ID: V_ON_KEYCODE_MODIFIER
Description: `v-on` no longer supports keyCode modifiers.
Old: `<input @keyup.13="submit" />`
New: `<input @keyup.enter="submit" />` or check `event.keyCode` manually.
```

--------------------------------

### Vue 3 Event Bus Replacement with tiny-emitter

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/breaking-changes/events-api.md

Shows how to replicate the Vue 2.x event bus API (`$on`, `$once`, `$off`, `$emit`) in Vue 3 using an external library like `tiny-emitter`. This provides a compatible interface for global event communication, though alternative patterns are generally encouraged.

```javascript
import emitter from 'tiny-emitter/instance'

export default {
  $on: (...args) => emitter.on(...args),
  $once: (...args) => emitter.once(...args),
  $off: (...args) => emitter.off(...args),
  $emit: (...args) => emitter.emit(...args)
}
```

--------------------------------

### Vue 2.x v-model Default Behavior

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/breaking-changes/v-model.md

Illustrates the default behavior of `v-model` on custom components in Vue 2.x, which implicitly binds to the `value` prop and listens for the `input` event.

```html
<ChildComponent v-model="pageTitle" />

<!-- would be shorthand for: -->

<ChildComponent :value="pageTitle" @input="pageTitle = $event" />
```

--------------------------------

### Vue 3 Migration: INSTANCE_SCOPED_SLOTS

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/migration-build.md

The instance property `vm.$scopedSlots` has been removed in Vue 3. `vm.$slots` now exposes functions for both regular and scoped slots, unifying the slot API.

```APIDOC
Change ID: INSTANCE_SCOPED_SLOTS
Description: `vm.$scopedSlots` has been removed; `vm.$slots` now exposes functions for all slots.
```

--------------------------------

### Vue 2 Custom Directive Lifecycle Hooks Reference

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/breaking-changes/custom-directives.md

Detailed reference for the optional lifecycle hooks available for custom directives in Vue 2, including their call timing and purpose.

```APIDOC
Vue 2 Custom Directive Hooks:
  bind: Called once the directive is bound to the element. Called only once.
  inserted: Called once the element is inserted into the parent DOM.
  update: Called when the element updates, but children haven't been updated yet.
  componentUpdated: Called once the component and the children have been updated.
  unbind: Called once the directive is removed. Also called only once.
```

--------------------------------

### Vue 3 Migration: GLOBAL_SET

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/migration-build.md

The global `Vue.set` method has been removed in Vue 3. It is no longer needed due to Vue 3's new reactivity system, which automatically detects property additions.

```APIDOC
Change ID: GLOBAL_SET
Description: `Vue.set` has been removed.
Reason: No longer needed due to Vue 3's reactivity system.
```

--------------------------------

### Vue 3.x: Placing `key` on `<template>` tag for `v-for`

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/breaking-changes/key-attribute.md

In Vue 3.x, the `key` attribute for `<template v-for>` should now be placed directly on the `<template>` tag itself. This simplifies key management for list rendering and is the recommended approach.

```HTML
<template v-for="item in list" :key="item.id">
  <div>...</div>
  <span>...</span>
</template>
```

--------------------------------

### Vue 3 Migration: GLOBAL_DELETE

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/migration-build.md

The global `Vue.delete` method has been removed in Vue 3. It is no longer needed as Vue 3's reactivity system handles property deletions automatically.

```APIDOC
Change ID: GLOBAL_DELETE
Description: `Vue.delete` has been removed.
Reason: No longer needed due to Vue 3's reactivity system.
```

--------------------------------

### Vue 3 Root Component Static Event Listener

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/breaking-changes/events-api.md

Illustrates how to add static event listeners directly to the root component in Vue 3. This is achieved by passing event handler functions as props to the `createApp` function.

```javascript
createApp(App, {
  // Listen for the 'expand' event
  onExpand() {
    console.log('expand')
  }
})
```

--------------------------------

### Vue 2.x Custom v-model with model Option

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/breaking-changes/v-model.md

Demonstrates how to customize the prop and event names for `v-model` in Vue 2.x using the `model` component option, allowing `value` to be used for other purposes. This also shows the resulting shorthand.

```html
<!-- ParentComponent.vue -->

<ChildComponent v-model="pageTitle" />
```

```javascript
// ChildComponent.vue

export default {
  model: {
    prop: 'title',
    event: 'change'
  },
  props: {
    // this allows using the `value` prop for a different purpose
    value: String,
    // use `title` as the prop which take the place of `value`
    title: {
      type: String,
      default: 'Default title'
    }
  }
}
```

```html
<ChildComponent :title="pageTitle" @change="pageTitle = $event" />
```

--------------------------------

### Vue 3 Migration: WATCH_ARRAY

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/migration-build.md

In Vue 3, watching an array no longer triggers on mutation by default unless the `deep` option is explicitly set to `true`.

```APIDOC
Change ID: WATCH_ARRAY
Description: Watching an array no longer triggers on mutation unless `deep` is true.
Old Behavior: `watch(myArray, handler)` would trigger on `myArray.push()`
New Behavior: `watch(myArray, handler)` requires `{ deep: true }` for array mutations.
```

--------------------------------

### Mounting a Vue 3 Application Instance

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/breaking-changes/global-api.md

Shows how to initialize a Vue 3 application instance using `createApp` and then mount a root component to a specified DOM target using `app.mount()`, making the application visible.

```js
import { createApp } from 'vue'
import MyApp from './MyApp.vue'

const app = createApp(MyApp)
app.mount('#app')
```

--------------------------------

### Vue 3 Accessing Component Instance in Custom Directive

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/breaking-changes/custom-directives.md

Illustrates how to access the component instance (`vm`) from within a custom directive's `mounted` hook in Vue 3. The instance is now available via `binding.instance`.

```javascript
mounted(el, binding, vnode) {
  const vm = binding.instance
}
```

--------------------------------

### Vue 2 Functional Component using SFC Template

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/breaking-changes/functional-components.md

Example of a functional component in Vue 2 using a Single File Component (SFC) with the `functional` attribute on the `<template>` tag. This approach allowed for a template-based syntax for functional components.

```vue
<template functional>
  <component
    :is="`h${props.level}`"
    v-bind="attrs"
    v-on="listeners"
  />
</template>

<script>
export default {
  props: ['level']
}
</script>
```

--------------------------------

### Vue 3 Custom Directive Lifecycle Hooks Mapping and Reference

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/breaking-changes/custom-directives.md

Comprehensive reference for the new and renamed lifecycle hooks for custom directives in Vue 3. It highlights their alignment with component lifecycle methods and indicates their Vue 2 equivalents.

```APIDOC
Vue 3 Custom Directive Hooks:
  created: New hook, called before the element's attributes or event listeners are applied.
  beforeMount: Replaces 'bind'.
  mounted: Replaces 'inserted'.
  beforeUpdate: New hook, called before the element itself is updated, much like component lifecycle hooks.
  updated: Replaces 'componentUpdated'. 'update' is removed due to redundancy.
  beforeUnmount: New hook, called right before an element is unmounted.
  unmounted: Replaces 'unbind'.
```

--------------------------------

### Vue 2 Accessing Component Instance in Custom Directive

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/breaking-changes/custom-directives.md

Demonstrates how to access the component instance (`vm`) from within a custom directive's `bind` hook in Vue 2. The instance is available via `vnode.context`.

```javascript
bind(el, binding, vnode) {
  const vm = vnode.context
}
```

--------------------------------

### Vue 2 Custom Directive Definition and Usage

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/breaking-changes/custom-directives.md

Demonstrates how to define and apply a custom directive in Vue 2. The `bind` hook is used to set an element's background style based on the directive's value.

```html
<p v-highlight="'yellow'">Highlight this text bright yellow</p>
```

```javascript
Vue.directive('highlight', {
  bind(el, binding, vnode) {
    el.style.background = binding.value
  }
})
```

--------------------------------

### Vue 3.x Custom v-model Modifiers on Components

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/breaking-changes/v-model.md

Introduces the ability to create custom `v-model` modifiers in Vue 3.x, allowing developers to extend `v-model` behavior beyond built-in modifiers like `.trim`.

```html
<ChildComponent v-model.capitalize="pageTitle" />
```

--------------------------------

### Vue 2.x: Using `key` on `v-if`/`v-else` branches

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/breaking-changes/key-attribute.md

In Vue 2.x, it was recommended to explicitly use `key` attributes on `v-if`/`v-else` branches. This helped Vue's virtual DOM algorithm track node identity and optimize rendering.

```HTML
<div v-if="condition" key="yes">Yes</div>
<div v-else key="no">No</div>
```

--------------------------------

### Vue 2 Functional Component using JavaScript

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/breaking-changes/functional-components.md

Example of a functional component in Vue 2 using a plain JavaScript object with the `functional: true` option and a `render` function. This component dynamically renders an HTML heading based on the 'level' prop.

```js
export default {
  functional: true,
  props: ['level'],
  render(h, { props, data, children }) {
    return h(`h${props.level}`, data, children)
  }
}
```

--------------------------------

### Vue 3 Functional Component using JavaScript

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/breaking-changes/functional-components.md

Example of a functional component in Vue 3 created with a plain JavaScript function. It receives `props` and `context` (containing `attrs`, `slots`, `emit`) as arguments, and the `h` (render function) utility is now imported globally.

```js
import { h } from 'vue'

const DynamicHeading = (props, context) => {
  return h(`h${props.level}`, context.attrs, context.slots)
}

DynamicHeading.props = ['level']

export default DynamicHeading
```

--------------------------------

### Vue 2.x Application Mounting with `el` or `$mount`

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/breaking-changes/mount-changes.md

This JavaScript snippet demonstrates how Vue 2.x applications are initialized and mounted. It shows two common patterns: using the `el` option directly in the constructor or calling `$mount()` on an application instance. In Vue 2.x, the rendered template content replaces the entire target HTML element.

```javascript
new Vue({
  el: '#app',
  data() {
    return {
      message: 'Hello Vue!'
    }
  },
  template: `
    <div id="rendered">{{ message }}</div>
  `
})

// or
const app = new Vue({
  data() {
    return {
      message: 'Hello Vue!'
    }
  },
  template: `
    <div id="rendered">{{ message }}</div>
  `
})

app.$mount('#app')
```

--------------------------------

### Migrating from Vue.extend to createApp for Component Instantiation in Vue 3

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/breaking-changes/global-api.md

In Vue 3, `Vue.extend` is removed as the concept of component constructors no longer exists. Component mounting should now use the `createApp` global API, simplifying component instantiation.

```js
// before - Vue 2

// create constructor
const Profile = Vue.extend({
  template: '<p>{{firstName}} {{lastName}} aka {{alias}}</p>',
  data() {
    return {
      firstName: 'Walter',
      lastName: 'White',
      alias: 'Heisenberg'
    }
  }
})
// create an instance of Profile and mount it on an element
new Profile().$mount('#mount-point')
```

```js
// after - Vue 3
const Profile = {
  template: '<p>{{firstName}} {{lastName}} aka {{alias}}</p>',
  data() {
    return {
      firstName: 'Walter',
      lastName: 'White',
      alias: 'Heisenberg'
    }
  }
}

Vue.createApp(Profile).mount('#mount-point')
```

--------------------------------

### Vue 3.x Component VNode Lifecycle Event Listener

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/breaking-changes/vnode-lifecycle-events.md

Example of attaching a VNode lifecycle event listener in Vue 3.x. The event name is now prefixed with "vue:", replacing "hook:". This syntax also applies to HTML elements.

```html
<template>
  <child-component @vue:updated="onUpdated">
</template>
```

--------------------------------

### Vue 3.x v-model Default modelValue Prop and update:modelValue Event

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/breaking-changes/v-model.md

Shows the new default prop (`modelValue`) and event (`update:modelValue`) names for `v-model` on custom components in Vue 3.x, standardizing the two-way binding API.

```html
<ChildComponent v-model="pageTitle" />

<!-- would be shorthand for: -->

<ChildComponent
  :modelValue="pageTitle"
  @update:modelValue="pageTitle = $event"
/>
```

--------------------------------

### Vue 2.x Component VNode Lifecycle Event Listener

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/breaking-changes/vnode-lifecycle-events.md

Example of attaching a VNode lifecycle event listener in Vue 2.x. The event name is prefixed with "hook:", followed by the lifecycle hook name, such as "updated".

```html
<template>
  <child-component @hook:updated="onUpdated">
</template>
```

--------------------------------

### Vue 3.x: Alternate solution for unique `key`s on conditional branches

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/breaking-changes/key-attribute.md

If manual `key`s are still desired for `v-if`/`v-else` branches in Vue 3.x, each branch must use a unique `key`. This ensures proper identification and avoids the breaking change introduced by duplicate keys.

```HTML
<div v-if="condition" key="a">Yes</div>
<div v-else key="b">No</div>
```

--------------------------------

### Vue 3 Functional Component using SFC Template

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/breaking-changes/functional-components.md

Example of a functional component in Vue 3 using a Single File Component (SFC). The `functional` attribute is removed from the `<template>` tag, and `props` and `attrs` are now accessed via `$props` and `$attrs` respectively. Listeners are now part of `$attrs`.

```vue
<template>
  <component
    v-bind:is="`h${$props.level}`"
    v-bind="$attrs"
  />
</template>

<script>
export default {
  props: ['level']
}
</script>
```

--------------------------------

### Using Provide/Inject with Vue 3 App Instance

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/breaking-changes/global-api.md

Demonstrates how a Vue 3 app instance can `provide` dependencies that can then be `inject`ed by any child component within that app, serving as a powerful alternative to `globalProperties` for plugins and cross-component communication.

```js
// in the entry
app.provide('guide', 'Vue 3 Guide')

// in a child component
export default {
  inject: {
    book: {
      from: 'guide'
    }
  },
  template: '<div>{{ book }}</div>'
}
```

--------------------------------

### Vue 3 Custom Directive Lifecycle Hooks Object Definition

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/breaking-changes/custom-directives.md

Illustrates the structure of the new unified lifecycle hooks object for custom directives in Vue 3, aligning with component lifecycle methods. Includes new hooks like `created`, `beforeUpdate`, and `beforeUnmount`.

```javascript
const MyDirective = {
  created(el, binding, vnode, prevVnode) {}, // new
  beforeMount() {},
  mounted() {},
  beforeUpdate() {}, // new
  updated() {},
  beforeUnmount() {}, // new
  unmounted() {}
}
```

--------------------------------

### Vue 3.x: Recommended solution for duplicate `key`s on conditional branches

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/breaking-changes/key-attribute.md

To resolve the breaking change of duplicate `key`s on `v-if`/`v-else` branches in Vue 3.x, the recommended approach is to remove the `key` attributes entirely. Vue now handles key generation automatically, making manual keys redundant in most cases.

```HTML
<div v-if="condition">Yes</div>
<div v-else>No</div>
```

--------------------------------

### Vue 2.x: Placing `key` on children within `<template v-for>`

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/breaking-changes/key-attribute.md

In Vue 2.x, the `<template>` tag could not have a `key` attribute directly. Instead, `key` attributes were placed on the individual children elements within a `<template v-for>` block to maintain state.

```HTML
<template v-for="item in list">
  <div :key="'heading-' + item.id">...</div>
  <span :key="'content-' + item.id">...</span>
</template>
```

--------------------------------

### Vue 3.x: Omitting `key` on `v-if`/`v-else` branches

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/breaking-changes/key-attribute.md

Vue 3.x automatically generates unique `key`s for conditional branches. This makes explicit `key` attributes unnecessary and no longer recommended for `v-if`/`v-else` blocks.

```HTML
<div v-if="condition">Yes</div>
<div v-else>No</div>
```

--------------------------------

### Vue 2.x: `key` on children with `<template v-for>` and `v-if`

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/breaking-changes/key-attribute.md

In Vue 2.x, when combining `<template v-for>` with conditional rendering (`v-if`/`v-else`), `key` attributes were placed on the individual child elements. This was necessary even if they were nested within a `<template>` tag.

```HTML
<template v-for="item in list">
  <div v-if="item.isVisible" :key="item.id">...</div>
  <span v-else :key="item.id">...</span>
</template>
```

--------------------------------

### Vue 2.x: Using duplicate `key`s on conditional branches

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/breaking-changes/key-attribute.md

In Vue 2.x, it was possible to intentionally use the same `key` on `v-if`/`v-else` branches. This practice forced branch reuse, but it is a breaking change in Vue 3.x and will lead to errors or unexpected behavior.

```HTML
<div v-if="condition" key="a">Yes</div>
<div v-else key="a">No</div>
```

--------------------------------

### Vue 3.x: `key` on `<template>` with `v-for` and `v-if`

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/breaking-changes/key-attribute.md

In Vue 3.x, when using `<template v-for>` with conditional rendering (`v-if`/`v-else`), the `key` attribute should be moved up to the `<template>` tag. Individual child elements no longer require keys in this scenario, streamlining the template structure.

```HTML
<template v-for="item in list" :key="item.id">
  <div v-if="item.isVisible">...</div>
  <span v-else>...</span>
</template>
```

--------------------------------

### Vue 2 Transition Group with Custom Tag

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/breaking-changes/transition-group.md

Demonstrates the Vue 2 syntax for `<transition-group>` where a root element (default `<span>`) was always rendered and could be customized using the `tag` attribute. This example explicitly sets `tag="ul"` for the list items.

```html
<transition-group tag="ul">
  <li v-for="item in items" :key="item">
    {{ item }}
  </li>
</transition-group>
```

--------------------------------

### Add TypeScript Declaration for Vue 3 Compat Module Augmentation

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/migration-build.md

This TypeScript declaration (`*.d.ts`) file augments the 'vue' module, exposing `CompatVue` as the default export and re-exporting from `@vue/runtime-dom`, which is crucial for correct type inference when migrating TypeScript projects to Vue 3 with `@vue/compat`.

```ts
declare module 'vue' {
  import { CompatVue } from '@vue/runtime-dom'
  const Vue: CompatVue
  export default Vue
  export * from '@vue/runtime-dom'
  const { configureCompat } = Vue
  export { configureCompat }
}
```

--------------------------------

### Vue 3.x Application Mounting with `createApp` and `mount`

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/breaking-changes/mount-changes.md

This JavaScript snippet illustrates the Vue 3.x approach to application mounting. It uses `Vue.createApp()` to create an application instance and then `app.mount()` to attach it to a target HTML element. Unlike Vue 2.x, the rendered content in Vue 3.x replaces the `innerHTML` of the target element, becoming its child.

```javascript
const app = Vue.createApp({
  data() {
    return {
      message: 'Hello Vue!'
    }
  },
  template: `
    <div id="rendered">{{ message }}</div>
  `
})

app.mount('#app')
```

--------------------------------

### Vue 3.x Template with Script Tag and Selector

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/breaking-changes/inline-template-attribute.md

Provides a migration path for Vue 3.x by defining component templates within a `<script type="text/html">` tag and referencing them via a selector in the component's `template` option. This method is suitable for no-build-tool setups.

```html
<script type="text/html" id="my-comp-template">
  <div>{{ hello }}</div>
</script>
```

```javascript
const MyComp = {
  template: '#my-comp-template'
  // ...
}
```

--------------------------------

### Vue 2.x Unit Testing with $nextTick for Async Components

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/breaking-changes/global-api-treeshaking.md

Illustrates using shallowMount and the instance method $nextTick() in Vue 2.x for unit testing async components. The instance method is a wrapper around Vue.nextTick(), and its inclusion contributes to non-tree-shakeable code.

```javascript
import { shallowMount } from '@vue/test-utils'
import { MyComponent } from './MyComponent.vue'

test('an async feature', async () => {
  const wrapper = shallowMount(MyComponent)

  // execute some DOM-related tasks

  await wrapper.vm.$nextTick()

  // run your assertions
})
```

--------------------------------

### Vue 2.x: `$attrs` and `inheritAttrs: false` with Class/Style

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/breaking-changes/attrs-includes-class-style.md

Illustrates the Vue 2.x behavior where `class` and `style` attributes are not included in `$attrs` when `inheritAttrs: false` is set. They are still applied to the component's root element, while other attributes are bound via `$attrs`. The example shows a component, its usage, and the resulting HTML.

```vue
<template>
  <label>
    <input type="text" v-bind="$attrs" />
  </label>
</template>
<script>
export default {
  inheritAttrs: false
}
</script>
```

```html
<my-component id="my-id" class="my-class"></my-component>
```

```html
<label class="my-class">
  <input type="text" id="my-id" />
</label>
```

--------------------------------

### Vue 3 Component Re-emitting Native Event Without Declaration

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/breaking-changes/emits-option.md

This example demonstrates a common migration pitfall in Vue 3. Re-emitting a native event (like 'click') without declaring it in `emits` can lead to the event being triggered twice by the parent due to the removal of the `.native` modifier.

```vue
<template>
  <button v-on:click="$emit('click', $event)">OK</button>
</template>
<script>
export default {
  emits: [] // without declared event
}
</script>
```

--------------------------------

### Watch Array Mutations with Deep Option in Vue 3.x

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/breaking-changes/watch.md

This Vue 3.x example demonstrates how to correctly watch for mutations within an array using the `deep: true` option. Without `deep: true`, the `handler` would only trigger if `bookList` was replaced entirely, not when its elements are added, removed, or modified.

```js
watch: {
  bookList: {
    handler(val, oldVal) {
      console.log('book list changed')
    },
    deep: true
  }
}
```

--------------------------------

### Migrate Vue 2 .sync Modifier to Vue 3 v-model

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/breaking-changes/v-model.md

This snippet illustrates the required syntax change for two-way binding on component props when migrating from Vue 2 to Vue 3. The `.sync` modifier is deprecated in Vue 3 and should be replaced with `v-model` using an argument for the bound prop.

```html
<ChildComponent :title.sync="pageTitle" />

<!-- to be replaced with -->

<ChildComponent v-model:title="pageTitle" />
```

--------------------------------

### Sharing Configurations Across Multiple Vue 3 App Instances

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/breaking-changes/global-api.md

Shows a factory function pattern to create multiple Vue 3 app instances that share common configurations, such as directives or components, ensuring consistency and reusability across different application roots.

```js
import { createApp } from 'vue'
import Foo from './Foo.vue'
import Bar from './Bar.vue'

const createMyApp = (options) => {
  const app = createApp(options)
  app.directive('focus' /* ... */)

  return app
}

createMyApp(Foo).mount('#foo')
createMyApp(Bar).mount('#bar')
```

--------------------------------

### Vue 3.x Migration: Enumerated Attribute IDL Value Changes

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/breaking-changes/attribute-coercion.md

This table outlines the IDL (Interface Description Language) attribute values for enumerated attributes when they are absent in Vue 3.x. It highlights how the actual state of attributes like `contenteditable`, `draggable`, and `spellcheck` is reflected, guiding developers on necessary v-bind adjustments for migration.

```APIDOC
| Absent enumerated attr | IDL attr & value                     |
| ---------------------- | ------------------------------------ |
| `contenteditable`      | `contentEditable` -> `'inherit'`     |
| `draggable`            | `draggable` -> `false`               |
| `spellcheck`           | `spellcheck` -> `true`               |
```

--------------------------------

### Vue 2.x Async Component with Options

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/breaking-changes/async-components.md

Illustrates the advanced syntax for defining async components in Vue 2.x using an options object, including delay, timeout, error, and loading components.

```js
const asyncModal = {
  component: () => import('./Modal.vue'),
  delay: 200,
  timeout: 3000,
  error: ErrorComponent,
  loading: LoadingComponent
}
```

--------------------------------

### Creating Vue 3 Application Instance (ES Module)

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/breaking-changes/global-api.md

Demonstrates the new `createApp` API in Vue 3 for creating an isolated application instance using ES module imports. This instance encapsulates its own configuration, preventing global state pollution.

```js
import { createApp } from 'vue'

const app = createApp({})
```

--------------------------------

### Creating Vue 3 Application Instance (CDN Global)

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/breaking-changes/global-api.md

Shows how to create a Vue 3 application instance when using Vue via a CDN, where `createApp` is available on the global `Vue` object. This method also creates an isolated app instance with its own configuration.

```js
const { createApp } = Vue

const app = createApp({})
```

--------------------------------

### Vue 3 Migration Strategy: Using Prop-Controlled Modal Component

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/breaking-changes/transition-as-root.md

Shows how to use the updated modal component in Vue 3, passing the `showModal` state as a prop to explicitly control the internal transition logic, aligning with the new behavior.

```html
<!-- usage -->
<modal :show="showModal">hello</modal>
```

--------------------------------

### Vue 2.x: Applying text formatting with filters

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/breaking-changes/filters.md

Demonstrates how filters were used in Vue 2.x to apply common text formatting, such as currency conversion, directly within templates. This approach required a custom syntax.

```html
<template>
  <h1>Bank Account Balance</h1>
  <p>{{ accountBalance | currencyUSD }}</p>
</template>

<script>
  export default {
    props: {
      accountBalance: {
        type: Number,
        required: true
      }
    },
    filters: {
      currencyUSD(value) {
        return '$' + value
      }
    }
  }
</script>
```

--------------------------------

### Vue 3 Migration Strategy: Prop-Controlled Modal Component

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/breaking-changes/transition-as-root.md

Demonstrates the recommended Vue 3 migration strategy to achieve similar transition effects for a root component. Instead of relying on the root `<transition>` directly, a `show` prop is introduced to control the internal `v-if` condition, explicitly managing the transition.

```vue
<template>
  <transition>
    <div v-if="show" class="modal"><slot/></div>
  </transition>
</template>
<script>
export default {
  props: ['show']
}
</script>
```

--------------------------------

### Vue 2.x vs 3.x Async Component Loader Function

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/breaking-changes/async-components.md

Compares the loader function signature between Vue 2.x and 3.x, showing that in 3.x, the loader function no longer receives `resolve` and `reject` arguments and must always return a Promise.

```js
// 2.x version
const oldAsyncComponent = (resolve, reject) => {
  /* ... */
}

// 3.x version
const asyncComponent = defineAsyncComponent(
  () =>
    new Promise((resolve, reject) => {
      /* ... */
    })
)
```

--------------------------------

### Registering Global Components and Directives on Vue 3 App Instance

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/breaking-changes/global-api.md

Illustrates how to register components and directives globally for a specific Vue 3 application instance using `app.component()` and `app.directive()`, ensuring they are available throughout that app's component tree without polluting the global environment.

```js
const app = createApp(MyApp)

app.component('button-counter', {
  data: () => ({
    count: 0
  }),
  template: '<button @click="count++">Clicked {{ count }} times.</button>'
})

app.directive('focus', {
  mounted: (el) => el.focus()
})

// now every application instance mounted with app.mount(), along with its
// component tree, will have the same “button-counter” component
// and “focus” directive without polluting the global environment
app.mount('#app')
```

--------------------------------

### Vue 2.x Async Component as Function

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/breaking-changes/async-components.md

Shows how an async component was defined in Vue 2.x as a simple function returning a promise.

```js
const asyncModal = () => import('./Modal.vue')
```

--------------------------------

### Vue 3.x Compiled Output for Transition and v-show

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/breaking-changes/global-api-treeshaking.md

The JavaScript output generated by the Vue 3.x compiler for a template using <transition> and v-show. It shows named imports for `h`, `Transition`, `withDirectives`, and `vShow`, enabling tree-shaking for these features.

```javascript
import { h, Transition, withDirectives, vShow } from 'vue'

export function render() {
  return h(Transition, [withDirectives(h('div', 'hello'), [[vShow, this.ok]])])
}
```

--------------------------------

### Vue 3.x Unit Testing with nextTick Named Export

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/breaking-changes/global-api-treeshaking.md

Demonstrates how to use the named export nextTick in Vue 3.x for unit testing async components, replacing the instance method $nextTick() for tree-shaking benefits and reduced bundle size.

```javascript
import { shallowMount } from '@vue/test-utils'
import { MyComponent } from './MyComponent.vue'
import { nextTick } from 'vue'

test('an async feature', async () => {
  const wrapper = shallowMount(MyComponent)

  // execute some DOM-related tasks

  await nextTick()

  // run your assertions
})
```

--------------------------------

### Vue 3.x: Using global filters via globalProperties in template

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/breaking-changes/filters.md

Demonstrates how to invoke global filter methods, registered via `globalProperties`, directly within Vue 3.x templates. This replaces the old filter syntax with a standard method call.

```html
<template>
  <h1>Bank Account Balance</h1>
  <p>{{ $filters.currencyUSD(accountBalance) }}</p>
</template>
```

--------------------------------

### Vue 3 v-on Kebab-Case Key Modifiers

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/breaking-changes/keycode-modifiers.md

Presents the recommended Vue 3 syntax for `v-on` key modifiers, using kebab-case names (e.g., `page-down`, `q`) instead of deprecated `keyCodes`.

```html
<!-- Vue 3 Key Modifier on v-on -->
<input v-on:keyup.page-down="nextPage">

<!-- Matches both q and Q -->
<input v-on:keydown.q="quit">
```

--------------------------------

### Replacing Vue.prototype with config.globalProperties in Vue 3

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/breaking-changes/global-api.md

Vue 3 replaces `Vue.prototype` with `config.globalProperties` for adding globally accessible properties to components. These properties are copied during component instantiation. `provide`/`inject` is also a recommended alternative.

```js
// before - Vue 2
Vue.prototype.$http = () => {}
```

```js
// after - Vue 3
const app = createApp({})
app.config.globalProperties.$http = () => {}
```

--------------------------------

### Vue 3.x defineAsyncComponent Usage

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/breaking-changes/async-components.md

Demonstrates the new `defineAsyncComponent` helper in Vue 3 for explicitly defining async components, both without and with options like `loader`, `delay`, `timeout`, `errorComponent`, and `loadingComponent`.

```js
import { defineAsyncComponent } from 'vue'
import ErrorComponent from './components/ErrorComponent.vue'
import LoadingComponent from './components/LoadingComponent.vue'

// Async component without options
const asyncModal = defineAsyncComponent(() => import('./Modal.vue'))

// Async component with options
const asyncModalWithOptions = defineAsyncComponent({
  loader: () => import('./Modal.vue'),
  delay: 200,
  timeout: 3000,
  errorComponent: ErrorComponent,
  loadingComponent: LoadingComponent
})
```

--------------------------------

### Vue 3.x: Using Multi-Root Components (Fragments)

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/new/fragments.md

Vue 3.x introduces official support for multi-root components, also known as fragments, eliminating the need for a single wrapper element. This allows templates to have multiple top-level nodes. However, it requires developers to explicitly define where attributes should be distributed using `v-bind="$attrs"`.

```html
<!-- Layout.vue -->
<template>
  <header>...</header>
  <main v-bind="$attrs">...</main>
  <footer>...</footer>
</template>
```

--------------------------------

### Vue 3.x: Registering global filters via globalProperties

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/breaking-changes/filters.md

Illustrates how to make globally registered filters available in Vue 3.x by attaching them to `app.config.globalProperties`. This allows existing filter logic to be reused as methods across components.

```javascript
// main.js
const app = createApp(App)

app.config.globalProperties.$filters = {
  currencyUSD(value) {
    return '$' + value
  }
}
```

--------------------------------

### Registering Global Component in Vue 2

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/breaking-changes/global-api.md

Demonstrates how to register a global component using the `Vue.component` API in Vue 2. This method globally mutates Vue's behavior, affecting all root instances created from the same Vue constructor.

```js
Vue.component('button-counter', {
  data: () => ({
    count: 0
  }),
  template: '<button @click="count++">Clicked {{ count }} times.</button>'
})
```

--------------------------------

### Demonstrating Global Mixin Impact on Multiple Vue 2 Apps

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/breaking-changes/global-api.md

Shows how a global mixin applied in Vue 2 affects all root instances created from the same Vue constructor. This highlights the difficulty of sharing the same copy of Vue between multiple applications with different global configurations.

```js
Vue.mixin({
  /* ... */
})

const app1 = new Vue({ el: '#app-1' })
const app2 = new Vue({ el: '#app-2' })
```

--------------------------------

### Parent Component Listening for Custom Event

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/breaking-changes/emits-option.md

Shows how a parent component listens for an event emitted by a child component using `v-on:click`.

```html
<my-button v-on:click="handleClick"></my-button>
```

--------------------------------

### Using createLocalVue for Isolated Testing in Vue 2

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/breaking-changes/global-api.md

Illustrates how `createLocalVue` from `vue-test-utils` is used to create an isolated Vue constructor for testing. This workaround helps prevent global configuration pollution during tests, addressing a limitation of Vue 2's global APIs.

```js
import { createLocalVue, mount } from '@vue/test-utils'

// create an extended `Vue` constructor
const localVue = createLocalVue()

// install a plugin “globally” on the “local” Vue constructor
localVue.use(MyPlugin)

// pass the `localVue` to the mount options
mount(Component, { localVue })
```

--------------------------------

### Vue 2.x: Wrapping Multi-Root Components in a Single Div

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/new/fragments.md

In Vue 2.x, multi-root components were not natively supported and would trigger a warning. Developers commonly wrapped all template elements within a single `<div>` to ensure a single root node and avoid this error. This snippet illustrates the typical Vue 2.x approach for layouts with multiple logical sections.

```html
<!-- Layout.vue -->
<template>
  <div>
    <header>...</header>
    <main>...</main>
    <footer>...</footer>
  </div>
</template>
```

--------------------------------

### Vue 3.x: Replacing filters with computed properties

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/breaking-changes/filters.md

Shows the recommended Vue 3.x approach to replace filters using computed properties for text formatting. This aligns with standard JavaScript expressions within templates.

```html
<template>
  <h1>Bank Account Balance</h1>
  <p>{{ accountInUSD }}</p>
</template>

<script>
  export default {
    props: {
      accountBalance: {
        type: Number,
        required: true
      }
    },
    computed: {
      accountInUSD() {
        return '$' + this.accountBalance
      }
    }
  }
</script>
```

--------------------------------

### Vue 2.x vs 3.x: Detailed Comparison of Attribute Binding Output

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/breaking-changes/attribute-coercion.md

This comprehensive table compares the HTML output generated by v-bind values for both enumerated and other non-boolean attributes between Vue 2.x and 3.x. It details the changes in coercion rules, helping developers understand and adapt their code to the new attribute handling logic in Vue 3.x.

```APIDOC
2.x "Enumerated attrs" (e.g. contenteditable, draggable, spellcheck):
  - 2.x v-bind: undefined -> 3.x v-bind: undefined, null -> HTML: removed
  - 2.x v-bind: true, 'true', '', 1, 'foo' -> 3.x v-bind: true, 'true' -> HTML: "true"
  - 2.x v-bind: null, false, 'false' -> 3.x v-bind: false, 'false' -> HTML: "false"

Other non-boolean attrs (e.g. aria-checked, tabindex, alt, etc.):
  - 2.x v-bind: undefined, null, false -> 3.x v-bind: undefined, null -> HTML: removed
  - 2.x v-bind: 'false' -> 3.x v-bind: false, 'false' -> HTML: "false"
```

--------------------------------

### Vue 2 v-on KeyCode and Alias Modifiers

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/breaking-changes/keycode-modifiers.md

Demonstrates the use of numeric `keyCode` and string aliases (like `enter`) as modifiers for `v-on` directives in Vue 2.

```html
<!-- keyCode version -->
<input v-on:keyup.13="submit" />

<!-- alias version -->
<input v-on:keyup.enter="submit" />
```

--------------------------------

### Vue 2.x CSS Transition Classes

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/breaking-changes/transition.md

CSS rules defining the `v-enter` and `v-leave` transition classes in Vue 2.x, showing their opacity states before the Vue 3 update. This syntax was considered confusing due to inconsistent naming.

```css
.v-enter,
.v-leave-to {
  opacity: 0;
}

.v-leave,
.v-enter-to {
  opacity: 1;
}
```

--------------------------------

### Migrating config.ignoredElements to config.compilerOptions.isCustomElement in Vue 3

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/breaking-changes/global-api.md

In Vue 3, `config.ignoredElements` is replaced by `config.compilerOptions.isCustomElement` for supporting native custom elements. The new option expects a function for more flexibility, unlike the old string/RegExp approach. This change affects template compilation and requires the runtime compiler.

```js
// before
Vue.config.ignoredElements = ['my-el', /^ion-/]
```

```js
// after
const app = createApp({})
app.config.compilerOptions.isCustomElement = (tag) => tag.startsWith('ion-')
```

--------------------------------

### Vue Render Registered Components

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/breaking-changes/render-function-api.md

Compares how registered components are rendered in Vue 2.x by passing a string name to `h`, versus Vue 3.x which requires explicit resolution using `resolveComponent` due to context-free VNodes.

```javascript
// 2.x
Vue.component('button-counter', {
  data() {
    return {
      count: 0
    }
  }
  template: `
    <button @click="count++">
      Clicked {{ count }} times.
    </button>
  `
})

export default {
  render(h) {
    return h('button-counter')
  }
}
```

```javascript
// 3.x
import { h, resolveComponent } from 'vue'

export default {
  setup() {
    const ButtonCounter = resolveComponent('button-counter')
    return () => h(ButtonCounter)
  }
}
```

--------------------------------

### Vue 3.x Global API Usage: nextTick Named Export

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/breaking-changes/global-api-treeshaking.md

Shows the Vue 3.x approach to accessing nextTick as a named export from 'vue', enabling tree-shaking. This replaces the direct Vue.nextTick() global access, optimizing bundle size.

```javascript
import { nextTick } from 'vue'

nextTick(() => {
  // something DOM-related
})
```

--------------------------------

### Rollup: Suppress External Dependency Warning for Vue

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/breaking-changes/global-api-treeshaking.md

Configuration for `rollup.config.js` showing how to use the `external` option to explicitly declare 'vue' as an external dependency, which suppresses the 'Treating vue as external dependency' warning during bundling.

```javascript
// rollup.config.js
export default {
  /*...*/
  external: ['vue']
}
```

--------------------------------

### Vue 2.x Component: Single Root Node Wrapper

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/uk/new/fragments.md

In Vue 2.x, components required a single root node, leading to the common practice of wrapping multiple elements within a <div> to avoid warnings. This snippet illustrates the typical structure for multi-element layouts in Vue 2.x.

```html
<!-- Layout.vue -->
<template>
  <div>
    <header>...</header>
    <main>...</main>
    <footer>...</footer>
  </div>
</template>
```

--------------------------------

### Vue 3.x CSS Transition Classes

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/breaking-changes/transition.md

Updated CSS rules for Vue 3.x transitions, renaming `v-enter` to `v-enter-from` and `v-leave` to `v-leave-from` for improved clarity and consistency with other class hook counterparts.

```css
.v-enter-from,
.v-leave-to {
  opacity: 0;
}

.v-leave-from,
.v-enter-to {
  opacity: 1;
}
```

--------------------------------

### Vue Render Function Argument and Import Changes

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/breaking-changes/render-function-api.md

Compares the `h` function handling in Vue 2.x where it was passed as an argument to the render function, versus Vue 3.x where it is globally imported from the 'vue' package.

```javascript
// Vue 2 Render Function Example
export default {
  render(h) {
    return h('div')
  }
}
```

```javascript
// Vue 3 Render Function Example
import { h } from 'vue'

export default {
  render() {
    return h('div')
  }
}
```

--------------------------------

### Vue.js: Passing Props to Root Component (2.x vs 3.x)

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/breaking-changes/props-data.md

Compares the method of passing props to a root Vue component instance. In Vue 2.x, the `propsData` option was used. In Vue 3.x, `propsData` is removed, and props are passed as the second argument to `createApp`.

```javascript
const Comp = Vue.extend({
  props: ['username'],
  template: '<div>{{ username }}</div>'
})

new Comp({
  propsData: {
    username: 'Evan'
  }
})
```

```javascript
const app = createApp(
  {
    props: ['username'],
    template: '<div>{{ username }}</div>'
  },
  { username: 'Evan' }
)
```

--------------------------------

### Vue 3.x Standardized Data Option Function Declaration

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/breaking-changes/data-option.md

Vue 3.x standardizes the `data` option to only accept a function that returns an object. This ensures consistent behavior across all component types, including root instances, and uses `createApp`.

```html
<script>
  import { createApp } from 'vue'

  createApp({
    data() {
      return {
        apiKey: 'a1b2c3'
      }
    }
  }).mount('#app')
</script>
```

--------------------------------

### Accessing Child Components with $children in Vue 2.x

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/breaking-changes/children.md

Demonstrates how to access direct child components using `this.$children` in Vue 2.x, showing its usage within a `mounted` lifecycle hook. This syntax is no longer supported in Vue 3.x.

```Vue
<template>
  <div>
    <img alt="Vue logo" src="./assets/logo.png">
    <my-button>Change logo</my-button>
  </div>
</template>

<script>
import MyButton from './MyButton'

export default {
  components: {
    MyButton
  },
  mounted() {
    console.log(this.$children) // [VueComponent]
  }
}
</script>
```

--------------------------------

### Vue 3 v-on Punctuation Key Modifiers

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/breaking-changes/keycode-modifiers.md

Demonstrates how to directly use certain punctuation marks (like comma) as key modifiers in Vue 3 `v-on` directives.

```html
<input v-on:keydown.,="commaPress">
```

--------------------------------

### Vue 2.x Global API Usage: Vue.nextTick

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/breaking-changes/global-api-treeshaking.md

Demonstrates how Vue.nextTick was accessed as a global API directly on the Vue object in Vue 2.x for DOM manipulation or async operations. This pattern is not tree-shakeable, leading to potential dead code in the final bundle.

```javascript
import Vue from 'vue'

Vue.nextTick(() => {
  // something DOM-related
})
```

--------------------------------

### Webpack: Exclude Vue from Plugin Bundle using Externals

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/breaking-changes/global-api-treeshaking.md

Configuration for `webpack.config.js` demonstrating how to use the `externals` option to prevent Vue's source code from being bundled into a plugin, treating 'vue' as an external dependency.

```javascript
// webpack.config.js
module.exports = {
  /*...*/
  externals: {
    vue: 'Vue'
  }
}
```

--------------------------------

### Vue Transition Component Prop Renames

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/breaking-changes/transition.md

API documentation for the renamed props of the `<transition>` component in Vue 3, reflecting the new transition class naming convention. These changes apply to both template and render function/JSX usage.

```APIDOC
Transition Component Prop Renames:
- `leave-class` is renamed to `leave-from-class` (can be written as `leaveFromClass` in render functions or JSX)
- `enter-class` is renamed to `enter-from-class` (can be written as `enterFromClass` in render functions or JSX)
```

--------------------------------

### Vue 2.x Global APIs Affected by Tree-shaking Changes

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/breaking-changes/global-api-treeshaking.md

Lists global APIs in Vue 2.x that are restructured in Vue 3.x for tree-shaking support. These APIs are no longer directly accessible on the global Vue object in ES Modules builds of Vue 3, requiring named imports instead.

```APIDOC
- Vue.nextTick
- Vue.observable (replaced by Vue.reactive)
- Vue.version
- Vue.compile (only in full builds)
- Vue.set (only in compat builds)
- Vue.delete (only in compat builds)
```

--------------------------------

### Vue 3.x Component: Multi-Root Node Fragments

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/uk/new/fragments.md

Vue 3.x officially supports components with multiple root nodes (fragments). This eliminates the need for a single wrapper element but requires explicit attribute distribution, often using v-bind="$attrs" on one of the root elements.

```html
<!-- Layout.vue -->
<template>
  <header>...</header>
  <main v-bind="$attrs"></main>
  <footer>...</footer>
</template>
```

--------------------------------

### Vue 2.x Behavior: External Toggling of Modal Component

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/breaking-changes/transition-as-root.md

Shows how the modal component, with a root `<transition>`, was toggled externally in Vue 2 using `v-if`. Toggling `showModal` would trigger a transition inside the modal component due to the old behavior.

```html
<!-- usage -->
<modal v-if="showModal">hello</modal>
```

--------------------------------

### Declaring Global Directive in Vue 2

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/breaking-changes/global-api.md

Shows how to declare a global directive using the `Vue.directive` API in Vue 2. Similar to global components, this approach also globally modifies Vue's behavior, impacting all Vue instances.

```js
Vue.directive('focus', {
  inserted: (el) => el.focus()
})
```

--------------------------------

### Vue 3.x Async Component Loader Option Renaming

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/breaking-changes/async-components.md

Highlights the renaming of the `component` option to `loader` within `defineAsyncComponent` options in Vue 3, emphasizing that a component definition cannot be provided directly.

```js
import { defineAsyncComponent } from 'vue'

const asyncModalWithOptions = defineAsyncComponent({
  loader: () => import('./Modal.vue'),
  delay: 200,
  timeout: 3000,
  errorComponent: ErrorComponent,
  loadingComponent: LoadingComponent
})
```

--------------------------------

### Vue.js Programmatic Slot Access (2.x vs 3.x)

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/breaking-changes/slots-unification.md

This snippet illustrates the change in how slots are accessed programmatically. In Vue 2.x, scoped slots were accessed via `this.$scopedSlots`. In Vue 3.x, all slots are unified under `this.$slots` and are accessed as functions, requiring a function call to retrieve their content.

```js
// 2.x Syntax
this.$scopedSlots.header
```

```js
// 3.x Syntax
this.$slots.header()
```

--------------------------------

### In-DOM Template Parsing Workarounds with `vue:` Prefix

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/breaking-changes/custom-elements-interop.md

For Vue templates directly written in HTML, native HTML parsing rules can restrict element nesting. In Vue 2.x, the `is` attribute on native tags was used as a workaround. Vue 3.x now requires a `vue:` prefix with `is` on native tags to explicitly resolve them as Vue components, maintaining compatibility while adhering to the new `is` behavior.

```html
<table>
  <tr is="blog-post-row"></tr>
</table>
```

```html
<table>
  <tr is="vue:blog-post-row"></tr>
</table>
```

--------------------------------

### Vue 2.x Behavior: Modal Component with Root Transition

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/breaking-changes/transition-as-root.md

Illustrates the Vue 2 behavior where a `<transition>` element used as the root of a component would implicitly trigger transitions when the component's visibility was toggled externally. This was an unintended side effect that is no longer supported in Vue 3.

```html
<!-- modal component -->
<template>
  <transition>
    <div class="modal"><slot/></div>
  </transition>
</template>
```

--------------------------------

### Vue 3.x: `$attrs` includes Class/Style with `inheritAttrs: false`

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/breaking-changes/attrs-includes-class-style.md

Demonstrates the Vue 3.x behavior where `$attrs` contains _all_ attributes, including `class` and `style`. This allows all attributes to be applied to a different element when `inheritAttrs: false` is used, changing the rendered HTML structure compared to Vue 2.x. This snippet shows the HTML output for the same component usage.

```html
<label>
  <input type="text" id="my-id" class="my-class" />
</label>
```

--------------------------------

### Vue VNode Props Format Changes

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/breaking-changes/render-function-api.md

Compares the VNode props structure between Vue 2.x, which used nested properties like `domProps` and `staticClass`, and Vue 3.x, which flattens the entire props structure for simplicity.

```javascript
// 2.x
{
  staticClass: 'button',
  class: {'is-outlined': isOutlined },
  staticStyle: { color: '#34495E' },
  style: { backgroundColor: buttonColor },
  attrs: { id: 'submit' },
  domProps: { innerHTML: '' },
  on: { click: submitForm },
  key: 'submit-button'
}
```

```javascript
// 3.x Syntax
{
  class: ['button', { 'is-outlined': isOutlined }],
  style: [{ color: '#34495E' }, { backgroundColor: buttonColor }],
  id: 'submit',
  innerHTML: '',
  onClick: submitForm,
  key: 'submit-button'
}
```

--------------------------------

### Vue 2.x Data Option Object and Function Declaration

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/breaking-changes/data-option.md

In Vue 2.x, the `data` option could be defined as either a plain JavaScript object or a function. This snippet shows both methods, which allowed for shared state in root instances but led to potential confusion.

```html
<!-- Object Declaration -->
<script>
  const app = new Vue({
    data: {
      apiKey: 'a1b2c3'
    }
  })
</script>
```

```html
<!-- Function Declaration -->
<script>
  const app = new Vue({
    data() {
      return {
        apiKey: 'a1b2c3'
      }
    }
  })
</script>
```

--------------------------------

### Vue 3 Props Default Function with Inject API

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/breaking-changes/props-default-this.md

Demonstrates how to define a prop with a default value factory function in Vue 3. It shows how the raw props are passed as an argument to the default function and how to use the 'inject' API to access injected properties, replacing the previous 'this' access.

```js
import { inject } from 'vue'

export default {
  props: {
    theme: {
      default (props) {
        // `props` is the raw values passed to the component,
        // before any type / default coercions
        // can also use `inject` to access injected properties
        return inject('theme', 'default-theme')
      }
    }
  }
}
```

--------------------------------

### Vue 3 Transition Group for Compatibility

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/breaking-changes/transition-group.md

Shows how to explicitly add `tag="span"` to `<transition-group>` in Vue 3 to maintain compatibility with Vue 2 styling or behaviors that relied on the default `<span>` root element. Vue 3 no longer renders a root element by default due to fragment support.

```html
<transition-group tag="span">
  <!-- -->
</transition-group>
```

--------------------------------

### Vue 2 Global KeyCode Alias Configuration

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/breaking-changes/keycode-modifiers.md

Illustrates how to define custom key aliases globally using `Vue.config.keyCodes` in Vue 2, mapping a custom name (e.g., `f1`) to a `keyCode`.

```javascript
Vue.config.keyCodes = {
  f1: 112
}
```

--------------------------------

### Vue 2 Custom KeyCode Alias Usage in Template

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/breaking-changes/keycode-modifiers.md

Shows how to use both the numeric `keyCode` and the custom alias defined via `config.keyCodes` as `v-on` modifiers in Vue 2 templates.

```html
<!-- keyCode version -->
<input v-on:keyup.112="showHelpText" />

<!-- custom alias version -->
<input v-on:keyup.f1="showHelpText" />
```

--------------------------------

### Customized Built-in Elements and `is` Attribute Behavior

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/breaking-changes/custom-elements-interop.md

Vue 3 restricts the special `is` attribute behavior to the `<component>` tag only. When `is` is used on plain HTML elements, it now behaves natively, supporting Customized Built-in Elements. This snippet illustrates the HTML syntax for such elements.

```html
<button is="plastic-button">Click Me!</button>
```

--------------------------------

### Vue.js Render Function Slot Definition (2.x vs 3.x)

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/breaking-changes/slots-unification.md

This snippet demonstrates the evolution of defining slots within render functions (`h`) from Vue 2.x to Vue 3.x. In 2.x, slots were defined using a `slot` data property on content nodes. In 3.x, slots are passed as an object of functions as children of the component node, unifying the approach.

```js
// 2.x Syntax
h(LayoutComponent, [
  h('div', { slot: 'header' }, this.header),
  h('div', { slot: 'content' }, this.content)
])
```

```js
// 3.x Syntax
h(LayoutComponent, {}, {
  header: () => h('div', this.header),
  content: () => h('div', this.content)
})
```

--------------------------------

### Vue 2 Component Event Emission

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/breaking-changes/emits-option.md

In Vue 2, components could emit events using `$emit` without explicit declaration. This snippet shows a basic component emitting an 'accepted' event.

```vue
<template>
  <div>
    <p>{{ text }}</p>
    <button v-on:click="$emit('accepted')">OK</button>
  </div>
</template>
<script>
  export default {
    props: ['text']
  }
</script>
```

--------------------------------

### Vue 2.x Attribute Coercion Behavior Table

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/breaking-changes/attribute-coercion.md

Illustrates how Vue 2.x coerces `v-bind` values for normal and enumerated attributes, showing the resulting HTML attribute based on different binding expressions. This table highlights inconsistencies in boolean handling in Vue 2.x.

```Vue Template
Binding expression  | foo (normal) | draggable (enumerated)
--------------------|--------------|-----------------------
:attr="null"        | -            | draggable="false"
:attr="undefined"   | -            | -
:attr="true"        | foo="true"   | draggable="true"
:attr="false"       | -            | draggable="false"
:attr="0"           | foo="0"      | draggable="true"
attr=""             | foo=""       | draggable="true"
attr="foo"          | foo="foo"    | draggable="true"
attr                | foo=""       | draggable="true"
```

--------------------------------

### Vue 2.x Inline Template Attribute Usage

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/breaking-changes/inline-template-attribute.md

Demonstrates the deprecated `inline-template` attribute in Vue 2.x, which allowed using the inner content of a component tag directly as its template, bypassing standard slot distribution.

```html
<my-component inline-template>
  <div>
    <p>These are compiled as the component's own template.</p>
    <p>Not parent's transclusion content.</p>
  </div>
</my-component>
```

--------------------------------

### Configuring Autonomous Custom Elements

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/breaking-changes/custom-elements-interop.md

Vue 3 changes how custom elements defined outside Vue (e.g., Web Components) are recognized. Previously configured via `Vue.config.ignoredElements`, this is now handled during template compilation. This snippet shows both Vue 2.x runtime configuration and Vue 3.x compile-time configuration (via `vue-loader` or `app.config.compilerOptions`).

```js
// This will make Vue ignore custom element defined outside of Vue
// (e.g., using the Web Components APIs)

Vue.config.ignoredElements = ['plastic-button']
```

```js
// in webpack config
rules: [
  {
    test: /\.vue$/,
    use: 'vue-loader',
    options: {
      compilerOptions: {
        isCustomElement: tag => tag === 'plastic-button'
      }
    }
  }
  // ...
]
```

```js
const app = Vue.createApp({})
app.config.compilerOptions.isCustomElement = tag => tag === 'plastic-button'
```

--------------------------------

### Vue 3.x Attribute Binding Behavior for Non-Boolean and Enumerated Attributes

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/breaking-changes/attribute-coercion.md

This table illustrates the new behavior of non-boolean HTML attributes, including enumerated attributes, in Vue 3.x. It shows how different v-bind expressions are coerced to specific HTML attribute values, addressing inconsistencies found in previous versions and allowing for more flexible attribute values.

```APIDOC
| Binding expression  | `foo` normal       | `draggable` enumerated |
| ------------------- | ------------------ | ---------------------- |
| `:attr="null"`      | -                  | - *                    |
| `:attr="undefined"` | -                  | -                      |
| `:attr="true"`      | `foo="true"`       | `draggable="true"`     |
| `:attr="false"`     | `foo="false"` *    | `draggable="false"`    |
| `:attr="0"`         | `foo="0"`          | `draggable="0"` *      |
| `attr=""`           | `foo=""`           | `draggable=""` *       |
| `attr="foo"`        | `foo="foo"`        | `draggable="foo"` *    |
| `attr`              | `foo=""`           | `draggable=""` *       |
```

--------------------------------

### Vue 3: Unified $attrs for attributes and event listeners with inheritAttrs: false

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/breaking-changes/listeners-removed.md

Shows the updated Vue 3 component syntax where event listeners are unified into the `$attrs` object. The `v-on` directive is no longer needed for fallthrough when `inheritAttrs: false` is used, as events are now attributes.

```vue
<template>
  <label>
    <input type="text" v-bind="$attrs" />
  </label>
</template>
<script>
export default {
  inheritAttrs: false
}
</script>
```

--------------------------------

### Vue Mixin Data Merge Behavior Change (2.x vs 3.x)

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/breaking-changes/data-option.md

This snippet demonstrates the change in `data` merging behavior when using mixins between Vue 2.x and Vue 3.x. Vue 2.x performed a deep merge of `data` properties, while Vue 3.x now performs a shallow merge, affecting how properties from mixins and components combine.

```javascript
const Mixin = {
  data() {
    return {
      user: {
        name: 'Jack',
        id: 1
      }
    }
  }
}

const CompA = {
  mixins: [Mixin],
  data() {
    return {
      user: {
        id: 2
      }
    }
  }
}
```

```json
{
  "user": {
    "id": 2,
    "name": "Jack"
  }
}
```

```json
{
  "user": {
    "id": 2
  }
}
```

--------------------------------

### Vue 2: Using $attrs and $listeners with inheritAttrs: false

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/breaking-changes/listeners-removed.md

Demonstrates the Vue 2 pattern for component attribute and event listener fallthrough. With `inheritAttrs: false`, `this.$attrs` and `this.$listeners` are explicitly bound to an inner element.

```vue
<template>
  <label>
    <input type="text" v-bind="$attrs" v-on="$listeners" />
  </label>
</template>
<script>
  export default {
    inheritAttrs: false
  }
</script>
```

--------------------------------

### Vue 3.x v-bind Merge Behavior (v-bind overrides)

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/breaking-changes/v-bind.md

In Vue 3.x, the order of how the bindings are declared determines how they are merged. If `v-bind="object"` is declared after an individual attribute, it will override the individual attribute. This snippet shows `v-bind="{ id: 'blue' }"` overriding `id="red"`.

```html
<!-- template -->
<div id="red" v-bind="{ id: 'blue' }"></div>
<!-- result -->
<div id="blue"></div>
```

--------------------------------

### Vue 3: Event listeners as part of $attrs object

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/breaking-changes/listeners-removed.md

Illustrates the structure of the `$attrs` object in Vue 3, where event listeners are now included as attributes prefixed with `on`.

```js
{
  text: 'this is an attribute',
  onClose: () => console.log('close Event triggered')
}
```

--------------------------------

### Vue 3.x v-bind Merge Behavior (individual attribute overrides)

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/breaking-changes/v-bind.md

In Vue 3.x, the order of how the bindings are declared determines how they are merged. If an individual attribute is declared after `v-bind="object"`, it will override the `v-bind` attribute. This snippet shows `id="red"` overriding `v-bind="{ id: 'blue' }"`.

```html
<!-- template -->
<div v-bind="{ id: 'blue' }" id="red"></div>
<!-- result -->
<div id="red"></div>
```

--------------------------------

### Vue 3 Component with `emits` Option

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/breaking-changes/emits-option.md

Vue 3 introduces the `emits` option to explicitly declare events a component can emit, similar to `props`. This improves clarity and allows for event validation, which can be defined by passing an object to `emits`.

```vue
<template>
  <div>
    <p>{{ text }}</p>
    <button v-on:click="$emit('accepted')">OK</button>
  </div>
</template>
<script>
  export default {
    props: ['text'],
    emits: ['accepted']
  }
</script>
```

--------------------------------

### Vue 2.x v-bind Merge Behavior

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/breaking-changes/v-bind.md

In Vue 2.x, if an element has both `v-bind="object"` and an identical individual attribute defined, the individual attribute would always overwrite bindings in the `object`. This snippet demonstrates how `id="red"` takes precedence over `v-bind="{ id: 'blue' }"`, resulting in `id="red"`.

```html
<!-- template -->
<div id="red" v-bind="{ id: 'blue' }"></div>
<!-- result -->
<div id="red"></div>
```

--------------------------------

### Vue 3.x Component Refactoring with Default Slot

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/breaking-changes/inline-template-attribute.md

Illustrates refactoring a Vue 2.x `inline-template` component to use a default slot in Vue 3.x. This approach makes data scoping explicit by passing child state through the slot, maintaining inline content convenience.

```html
<!-- 2.x Syntax -->
<my-comp inline-template :msg="parentMsg">
  {{ msg }} {{ childState }}
</my-comp>

<!-- Default Slot Version -->
<my-comp v-slot="{ childState }">
  {{ parentMsg }} {{ childState }}
</my-comp>
```

```html
<!--
  in child template, render default slot while passing
  in necessary private state of child.
-->
<template>
  <slot :childState="childState" />
</template>
```

--------------------------------

### Vue 2.x: Using v-on.native for DOM Events

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/breaking-changes/v-on-native-modifier-removed.md

In Vue 2.x, the `.native` modifier was used with `v-on` to attach a native DOM event listener directly to the root element of a child component, distinct from custom component events.

```html
<my-component
  v-on:close="handleComponentEvent"
  v-on:click.native="handleNativeClickEvent"
/>
```

--------------------------------

### Vue 3.x: Declaring Emitted Events with `emits` Option

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/breaking-changes/v-on-native-modifier-removed.md

Vue 3 components should declare all custom events they emit using the `emits` option. This clarifies the component's API and influences how `v-on` listeners are handled by the parent.

```vue
<script>
  export default {
    emits: ['close']
  }
</script>
```

--------------------------------

### Vue 3.x: v-on Fallthrough for Native Events

Source: https://github.com/vuejs/v3-migration-guide/blob/main/src/breaking-changes/v-on-native-modifier-removed.md

In Vue 3, the `.native` modifier is removed. Event listeners not declared in the child component's `emits` option are automatically applied as native DOM listeners to the child's root element.

```html
<my-component
  v-on:close="handleComponentEvent"
  v-on:click="handleNativeClickEvent"
/>
```

=== COMPLETE CONTENT === This response contains all available snippets from this library. No additional content exists. Do not make further requests.