# Vue Router 3.x

Vue Router is the official routing library for Vue.js 2. It enables navigation between views in Single Page Applications (SPAs) by mapping URL paths to Vue components. The router deeply integrates with Vue.js core, providing a seamless developer experience for building complex client-side applications with features like nested route/view mapping, dynamic route matching, and navigation guards.

Vue Router 3.x supports three routing modes: hash mode (using URL hash), history mode (using HTML5 History API), and abstract mode (for non-browser environments like Node.js). It offers declarative navigation through `<router-link>` components and programmatic navigation through the router instance methods. The library also provides navigation guards for authentication, data fetching, and scroll behavior customization.

## Installation and Setup

Install Vue Router via npm and register it as a Vue plugin to enable routing capabilities in your application.

```bash
npm install vue-router
```

```js
import Vue from 'vue'
import VueRouter from 'vue-router'

// Register the plugin
Vue.use(VueRouter)

// Define route components
const Home = { template: '<div>Home</div>' }
const About = { template: '<div>About</div>' }
const User = { template: '<div>User {{ $route.params.id }}</div>' }

// Create router instance with routes configuration
const router = new VueRouter({
  mode: 'history', // Use HTML5 history mode (removes # from URLs)
  base: '/', // Base URL of the app
  routes: [
    { path: '/', component: Home },
    { path: '/about', component: About },
    { path: '/user/:id', component: User }
  ]
})

// Create and mount the root instance
const app = new Vue({
  router
}).$mount('#app')

// Access router and route in components:
// this.$router - the router instance
// this.$route - the current route object
```

## Router-Link Component

The `<router-link>` component enables declarative navigation between routes. It renders as an `<a>` tag by default and automatically handles click events to prevent full page reloads.

```html
<template>
  <div id="app">
    <!-- Basic navigation -->
    <router-link to="/">Home</router-link>
    <router-link to="/about">About</router-link>

    <!-- Named route with params -->
    <router-link :to="{ name: 'user', params: { id: 123 }}">
      User Profile
    </router-link>

    <!-- With query parameters -->
    <router-link :to="{ path: '/search', query: { q: 'vue' }}">
      Search
    </router-link>

    <!-- Replace instead of push (no history entry) -->
    <router-link to="/settings" replace>Settings</router-link>

    <!-- Exact matching for active class -->
    <router-link to="/" exact>Home</router-link>

    <!-- Custom active class -->
    <router-link to="/dashboard" active-class="is-active">
      Dashboard
    </router-link>

    <!-- Using v-slot API for custom rendering (3.1.0+) -->
    <router-link
      to="/profile"
      custom
      v-slot="{ href, route, navigate, isActive, isExactActive }"
    >
      <li :class="{ 'active': isActive }">
        <a :href="href" @click="navigate">{{ route.fullPath }}</a>
      </li>
    </router-link>

    <!-- Route outlet - matched component renders here -->
    <router-view></router-view>
  </div>
</template>
```

## Programmatic Navigation

Navigate programmatically using the router instance methods. These methods work consistently across all router modes (history, hash, abstract).

```js
export default {
  methods: {
    navigateToUser() {
      // Navigate using string path
      this.$router.push('/user/123')

      // Navigate using location object
      this.$router.push({ path: '/user/123' })

      // Navigate using named route with params
      this.$router.push({ name: 'user', params: { id: '123' } })

      // Navigate with query parameters
      this.$router.push({
        path: '/search',
        query: { q: 'vue', page: 1 }
      })

      // Using promise (3.1.0+)
      this.$router.push('/dashboard')
        .then(() => {
          console.log('Navigation complete')
        })
        .catch(err => {
          // Handle navigation failures
          if (err.name === 'NavigationDuplicated') {
            // Navigated to same route
          }
        })
    },

    replaceRoute() {
      // Replace current history entry (no back button)
      this.$router.replace('/new-page')
      this.$router.replace({ name: 'newPage' })
    },

    historyNavigation() {
      // Go forward one step
      this.$router.go(1)
      // Equivalent to router.forward()
      this.$router.forward()

      // Go back one step
      this.$router.go(-1)
      // Equivalent to router.back()
      this.$router.back()

      // Go forward 3 steps
      this.$router.go(3)
    }
  }
}
```

## Dynamic Route Matching

Define routes with dynamic segments using colon syntax. Parameters are accessible via `$route.params`.

```js
const router = new VueRouter({
  routes: [
    // Single dynamic segment
    { path: '/user/:id', component: User },

    // Multiple dynamic segments
    { path: '/user/:username/post/:postId', component: Post },

    // Optional parameter (using regex)
    { path: '/optional/:id?', component: OptionalParam },

    // Catch-all route (404)
    { path: '*', component: NotFound },

    // Catch-all with prefix
    { path: '/files-*', component: FileViewer }
  ]
})

// Component accessing route params
const User = {
  template: '<div>User ID: {{ $route.params.id }}</div>',

  // Watch for param changes (same component reused)
  watch: {
    '$route'(to, from) {
      // Fetch new user data when id changes
      this.fetchUser(to.params.id)
    }
  },

  // Or use beforeRouteUpdate guard
  beforeRouteUpdate(to, from, next) {
    this.fetchUser(to.params.id)
    next()
  },

  methods: {
    fetchUser(id) {
      // Fetch user data...
    }
  }
}

// Catch-all route provides pathMatch param
// URL: /files-documents/reports/2023
// $route.params.pathMatch === 'documents/reports/2023'
```

## Nested Routes

Define nested routes using the `children` option to render components inside parent component's `<router-view>`.

```js
const router = new VueRouter({
  routes: [
    {
      path: '/user/:id',
      component: User,
      children: [
        // Default child route (matches /user/:id)
        { path: '', component: UserHome },

        // Matches /user/:id/profile
        { path: 'profile', component: UserProfile },

        // Matches /user/:id/posts
        { path: 'posts', component: UserPosts },

        // Nested children can continue
        {
          path: 'settings',
          component: UserSettings,
          children: [
            { path: 'account', component: AccountSettings },
            { path: 'privacy', component: PrivacySettings }
          ]
        }
      ]
    }
  ]
})

// Parent component with nested router-view
const User = {
  template: `
    <div class="user">
      <h2>User {{ $route.params.id }}</h2>
      <nav>
        <router-link :to="'/user/' + $route.params.id">Home</router-link>
        <router-link :to="'/user/' + $route.params.id + '/profile'">Profile</router-link>
        <router-link :to="'/user/' + $route.params.id + '/posts'">Posts</router-link>
      </nav>
      <!-- Nested components render here -->
      <router-view></router-view>
    </div>
  `
}
```

## Named Routes and Views

Use named routes for easier navigation and named views for rendering multiple components at the same route.

```js
const router = new VueRouter({
  routes: [
    // Named route
    {
      path: '/user/:id',
      name: 'user',
      component: User
    },

    // Named views - multiple router-views at same level
    {
      path: '/dashboard',
      components: {
        default: Dashboard,
        sidebar: DashboardSidebar,
        header: DashboardHeader
      }
    },

    // Nested named views
    {
      path: '/settings',
      component: Settings,
      children: [
        {
          path: 'profile',
          components: {
            default: ProfileEditor,
            helper: ProfileHelp
          }
        }
      ]
    }
  ]
})

// Navigate using route name
this.$router.push({ name: 'user', params: { id: '123' } })

// Template with named views
// <template>
//   <div>
//     <router-view name="header"></router-view>
//     <router-view name="sidebar"></router-view>
//     <router-view></router-view> <!-- default -->
//   </div>
// </template>
```

## Navigation Guards

Control navigation flow using guards for authentication, data loading, and access control.

```js
const router = new VueRouter({
  routes: [
    {
      path: '/admin',
      component: Admin,
      meta: { requiresAuth: true },
      // Per-route guard
      beforeEnter: (to, from, next) => {
        if (!isAdmin()) {
          next({ name: 'forbidden' })
        } else {
          next()
        }
      }
    }
  ]
})

// Global before guard
router.beforeEach((to, from, next) => {
  // Check if route requires authentication
  if (to.matched.some(record => record.meta.requiresAuth)) {
    if (!isAuthenticated()) {
      next({
        path: '/login',
        query: { redirect: to.fullPath }
      })
    } else {
      next()
    }
  } else {
    next()
  }
})

// Global resolve guard (called after in-component guards)
router.beforeResolve((to, from, next) => {
  // Ensure data is loaded
  next()
})

// Global after hook (cannot affect navigation)
router.afterEach((to, from) => {
  // Analytics, update document title, etc.
  document.title = to.meta.title || 'Default Title'
})

// In-component guards
const UserProfile = {
  template: '...',

  beforeRouteEnter(to, from, next) {
    // Called before component is created
    // Does NOT have access to `this`
    // Can pass callback to access instance
    next(vm => {
      vm.loadData(to.params.id)
    })
  },

  beforeRouteUpdate(to, from, next) {
    // Called when route changes but component is reused
    // Has access to `this`
    this.loadData(to.params.id)
    next()
  },

  beforeRouteLeave(to, from, next) {
    // Called when navigating away
    // Useful for unsaved changes warning
    if (this.hasUnsavedChanges) {
      const answer = window.confirm('Discard unsaved changes?')
      if (answer) {
        next()
      } else {
        next(false) // Cancel navigation
      }
    } else {
      next()
    }
  }
}
```

## Route Meta Fields

Attach custom data to routes using the `meta` field for authentication, breadcrumbs, transitions, etc.

```js
const router = new VueRouter({
  routes: [
    {
      path: '/admin',
      component: Admin,
      meta: {
        requiresAuth: true,
        roles: ['admin', 'superadmin'],
        title: 'Admin Dashboard',
        transition: 'slide-left'
      },
      children: [
        {
          path: 'users',
          component: AdminUsers,
          meta: {
            requiresAuth: true,
            roles: ['admin'],
            title: 'User Management'
          }
        }
      ]
    }
  ]
})

// Access meta in guards
router.beforeEach((to, from, next) => {
  // Check all matched routes (including nested)
  const requiredRoles = to.matched
    .filter(record => record.meta.roles)
    .flatMap(record => record.meta.roles)

  if (requiredRoles.length > 0) {
    const userRoles = getCurrentUserRoles()
    const hasAccess = requiredRoles.some(role => userRoles.includes(role))

    if (!hasAccess) {
      next({ name: 'forbidden' })
      return
    }
  }

  next()
})

// Access meta in component
export default {
  computed: {
    pageTitle() {
      return this.$route.meta.title
    }
  }
}
```

## Passing Props to Route Components

Decouple components from the router by passing route params as props instead of using `$route` directly.

```js
const router = new VueRouter({
  routes: [
    // Boolean mode - passes route.params as props
    {
      path: '/user/:id',
      component: User,
      props: true
    },

    // Object mode - static props
    {
      path: '/promotion',
      component: Promotion,
      props: { discount: 20, featured: true }
    },

    // Function mode - dynamic props from route
    {
      path: '/search',
      component: Search,
      props: route => ({
        query: route.query.q,
        page: parseInt(route.query.page) || 1,
        filters: route.query.filters?.split(',') || []
      })
    },

    // Named views with different props modes
    {
      path: '/user/:id',
      components: {
        default: UserProfile,
        sidebar: UserSidebar
      },
      props: {
        default: true,
        sidebar: route => ({ userId: route.params.id })
      }
    }
  ]
})

// Component using props (decoupled from router)
const User = {
  props: ['id'],
  template: '<div>User: {{ id }}</div>',

  // Can be tested without router
  // Can be used with or without router
}
```

## Redirect and Alias

Configure redirects and aliases to map multiple paths to the same component or redirect users to different routes.

```js
const router = new VueRouter({
  routes: [
    // Simple redirect
    { path: '/home', redirect: '/' },

    // Redirect to named route
    { path: '/u/:id', redirect: { name: 'user' } },

    // Dynamic redirect with function
    {
      path: '/search/:term',
      redirect: to => {
        // Return redirect path/location
        return { path: '/results', query: { q: to.params.term } }
      }
    },

    // Alias - URL stays the same, content from aliased route
    {
      path: '/user/:id',
      component: User,
      alias: '/profile/:id'
      // Both /user/123 and /profile/123 show User component
      // URL remains unchanged
    },

    // Multiple aliases
    {
      path: '/dashboard',
      component: Dashboard,
      alias: ['/home', '/main', '/start']
    }
  ]
})
```

## Scroll Behavior

Customize scroll position when navigating between routes using the `scrollBehavior` option.

```js
const router = new VueRouter({
  routes: [...],

  scrollBehavior(to, from, savedPosition) {
    // savedPosition is available for popstate navigations (back/forward)
    if (savedPosition) {
      return savedPosition
    }

    // Scroll to hash anchor
    if (to.hash) {
      return {
        selector: to.hash,
        offset: { x: 0, y: 80 }, // Account for fixed header
        behavior: 'smooth'
      }
    }

    // Scroll to top for new routes
    if (to.matched.some(m => m.meta.scrollToTop)) {
      return { x: 0, y: 0 }
    }

    // Keep scroll position between sibling routes
    if (to.path.startsWith('/docs/') && from.path.startsWith('/docs/')) {
      return false // Don't scroll
    }

    return { x: 0, y: 0 }
  }
})

// Async scroll behavior (2.8.0+)
const router = new VueRouter({
  scrollBehavior(to, from, savedPosition) {
    return new Promise((resolve) => {
      // Wait for transition to complete
      setTimeout(() => {
        resolve({ x: 0, y: 0 })
      }, 300)
    })
  }
})
```

## Lazy Loading Routes

Split route components into separate chunks that are loaded on-demand when the route is visited.

```js
// Lazy load components using dynamic import
const Home = () => import('./views/Home.vue')
const About = () => import('./views/About.vue')
const User = () => import('./views/User.vue')

const router = new VueRouter({
  routes: [
    { path: '/', component: Home },
    { path: '/about', component: About },
    { path: '/user/:id', component: User }
  ]
})

// Group components into named chunks
const router = new VueRouter({
  routes: [
    {
      path: '/admin',
      component: () => import(/* webpackChunkName: "admin" */ './views/Admin.vue'),
      children: [
        {
          path: 'users',
          component: () => import(/* webpackChunkName: "admin" */ './views/AdminUsers.vue')
        },
        {
          path: 'settings',
          component: () => import(/* webpackChunkName: "admin" */ './views/AdminSettings.vue')
        }
      ]
    }
  ]
})

// With loading and error components
const AsyncComponent = () => ({
  component: import('./views/HeavyComponent.vue'),
  loading: LoadingComponent,
  error: ErrorComponent,
  delay: 200, // Show loading after 200ms
  timeout: 10000 // Timeout after 10s
})
```

## Route Object Properties

Access current route information through the `$route` object available in all components.

```js
export default {
  computed: {
    routeInfo() {
      return {
        // Current path
        path: this.$route.path, // '/user/123'

        // Dynamic segments
        params: this.$route.params, // { id: '123' }

        // Query string parameters
        query: this.$route.query, // { tab: 'posts', page: '1' }

        // URL hash
        hash: this.$route.hash, // '#section'

        // Full resolved URL
        fullPath: this.$route.fullPath, // '/user/123?tab=posts#section'

        // Route name (if defined)
        name: this.$route.name, // 'user'

        // Route meta fields (merged from all matched routes)
        meta: this.$route.meta, // { requiresAuth: true }

        // Array of matched route records
        matched: this.$route.matched,

        // Redirected from (if applicable)
        redirectedFrom: this.$route.redirectedFrom
      }
    }
  },

  watch: {
    // Watch entire route object
    '$route'(to, from) {
      console.log('Route changed:', to.path)
    },

    // Watch specific property
    '$route.query.page'(newPage) {
      this.loadPage(newPage)
    }
  }
}
```

## Dynamic Route Registration

Add and remove routes at runtime using `addRoute` and `getRoutes` methods.

```js
const router = new VueRouter({
  routes: [
    { path: '/', component: Home }
  ]
})

// Add a new route (3.5.0+)
const removeRoute = router.addRoute({
  path: '/dynamic',
  name: 'dynamic',
  component: DynamicPage
})

// Add nested route under existing parent
router.addRoute('user', {
  path: 'activity',
  component: UserActivity
})

// Remove the added route
removeRoute()

// Get all registered routes
const routes = router.getRoutes()
console.log(routes.map(r => r.path))

// Check if route exists and add if not
if (!router.getRoutes().find(r => r.name === 'newFeature')) {
  router.addRoute({
    path: '/new-feature',
    name: 'newFeature',
    component: () => import('./views/NewFeature.vue')
  })
}
```

## Composables (Vue 2.7+)

Use composition API composables for accessing router and route in Vue 2.7+ applications.

```js
import {
  useRouter,
  useRoute,
  useLink,
  onBeforeRouteUpdate,
  onBeforeRouteLeave
} from 'vue-router/composables'

export default {
  setup() {
    const router = useRouter()
    const route = useRoute()

    // Reactive access to route properties
    const userId = computed(() => route.params.id)
    const searchQuery = computed(() => route.query.q)

    // Programmatic navigation
    function goToUser(id) {
      router.push({ name: 'user', params: { id } })
    }

    // Navigation guards in setup
    onBeforeRouteUpdate((to, from, next) => {
      // Called when route params change
      console.log('Route updating:', to.params)
      next()
    })

    onBeforeRouteLeave((to, from, next) => {
      // Prevent leaving with unsaved changes
      if (hasUnsavedChanges.value) {
        const confirmed = confirm('Discard changes?')
        next(confirmed)
      } else {
        next()
      }
    })

    // useLink for custom link components
    const { href, route: linkRoute, navigate, isActive } = useLink({
      to: { name: 'dashboard' }
    })

    return {
      userId,
      searchQuery,
      goToUser,
      href,
      navigate,
      isActive
    }
  }
}
```

## Navigation Failures and Error Handling

Handle navigation errors and failures gracefully using promises and the `onError` callback.

```js
import VueRouter, { isNavigationFailure, NavigationFailureType } from 'vue-router'

const router = new VueRouter({ routes: [...] })

// Global error handler
router.onError(error => {
  console.error('Router error:', error)
  // Handle async component loading failures, etc.
})

// Handle navigation failures in component
export default {
  methods: {
    async navigate() {
      try {
        await this.$router.push('/protected')
      } catch (failure) {
        if (isNavigationFailure(failure, NavigationFailureType.redirected)) {
          // Navigation was redirected (e.g., by a guard)
          console.log('Redirected to:', failure.to.path)
        } else if (isNavigationFailure(failure, NavigationFailureType.aborted)) {
          // Navigation was aborted (guard returned false)
          console.log('Navigation aborted')
        } else if (isNavigationFailure(failure, NavigationFailureType.cancelled)) {
          // Navigation was cancelled by a new navigation
          console.log('Navigation cancelled')
        } else if (isNavigationFailure(failure, NavigationFailureType.duplicated)) {
          // Navigated to same route
          console.log('Already at this route')
        } else {
          // Unknown error
          throw failure
        }
      }
    }
  }
}

// Detect initial navigation
router.beforeEach((to, from) => {
  if (from === VueRouter.START_LOCATION) {
    // This is the initial navigation
    console.log('Initial navigation to:', to.path)
  }
})
```

## Transitions with Router View

Animate route transitions using Vue's `<transition>` component with `<router-view>`.

```html
<template>
  <!-- Basic transition -->
  <transition name="fade" mode="out-in">
    <router-view></router-view>
  </transition>

  <!-- Per-route transitions using meta -->
  <transition :name="transitionName" mode="out-in">
    <router-view></router-view>
  </transition>

  <!-- With keep-alive for caching -->
  <transition name="slide" mode="out-in">
    <keep-alive :include="cachedViews">
      <router-view :key="$route.fullPath"></router-view>
    </keep-alive>
  </transition>
</template>

<script>
export default {
  computed: {
    transitionName() {
      return this.$route.meta.transition || 'fade'
    },
    cachedViews() {
      return this.$route.meta.keepAlive ? [this.$route.name] : []
    }
  },
  watch: {
    '$route'(to, from) {
      // Dynamic transition based on route depth
      const toDepth = to.path.split('/').length
      const fromDepth = from.path.split('/').length
      this.transitionName = toDepth < fromDepth ? 'slide-right' : 'slide-left'
    }
  }
}
</script>

<style>
.fade-enter-active, .fade-leave-active {
  transition: opacity 0.3s ease;
}
.fade-enter, .fade-leave-to {
  opacity: 0;
}

.slide-left-enter-active, .slide-left-leave-active,
.slide-right-enter-active, .slide-right-leave-active {
  transition: transform 0.3s ease;
}
.slide-left-enter, .slide-right-leave-to {
  transform: translateX(100%);
}
.slide-left-leave-to, .slide-right-enter {
  transform: translateX(-100%);
}
</style>
```

## Summary

Vue Router 3.x is a comprehensive client-side routing solution designed specifically for Vue.js 2 applications. Its primary use cases include building single-page applications with multiple views, implementing authentication flows with navigation guards, creating nested layouts with child routes, and enabling code-splitting through lazy-loaded route components. The router supports various navigation patterns including programmatic navigation, declarative links, redirects, and aliases.

Integration with Vue applications follows a standard plugin pattern where the router instance is passed to the root Vue instance. Components gain access to routing through injected `$router` and `$route` properties, or via composables in Vue 2.7+. The router seamlessly works with Vue's reactivity system, transition components, and keep-alive caching. For complex applications, features like route meta fields, per-route guards, and dynamic route registration provide the flexibility needed for authentication, authorization, and feature flagging scenarios.
