# 🚀 Nuxt 3 Cheatsheet

A comprehensive cheatsheet for Nuxt 3 and Vue 3 development, featuring common patterns, best practices, and code examples.

## 🌟 Features

- Vue 3 Composition API examples
- Nuxt 3 specific features and patterns
- Common use cases and solutions
- TypeScript support
- Best practices and tips

## 🛠 Installation

```bash
# Create new project
npx nuxi init my-nuxt-app

# Install dependencies
cd my-nuxt-app
npm install

# Start development server
npm run dev
```

## 📚 Cheatsheet

### 🔥 Vue 3 Composition API

```vue
<script setup>
import { ref, computed, onMounted } from 'vue'

// Reactive state
const count = ref(0)

// Computed property
const doubleCount = computed(() => count.value * 2)

// Lifecycle hook
onMounted(() => {
  console.log('Component mounted')
})

// Method
const increment = () => count.value++
</script>

<template>
  <div>
    <p>Count: {{ count }}</p>
    <p>Double: {{ doubleCount }}</p>
    <button @click="increment">Increment</button>
  </div>
</template>
```

### 🎯 Nuxt 3 Features

#### Pages & Routing
```vue
// pages/index.vue - Auto-generated route: /
<template>
  <div>Home Page</div>
</template>

// pages/users/[id].vue - Dynamic route: /users/:id
<script setup>
const route = useRoute()
const id = route.params.id
</script>
```

#### Data Fetching
```vue
<script setup>
// Composable for data fetching
const { data: users } = await useFetch('/api/users')

// With options
const { data: posts } = await useFetch('/api/posts', {
  lazy: true,
  watch: true,
  transform: (posts) => posts.map(post => ({
    ...post,
    title: post.title.toUpperCase()
  }))
})
</script>
```

#### State Management
```vue
// composables/useState.ts
export const useCounter = () => useState('counter', () => 0)

// Component usage
<script setup>
const counter = useCounter()
</script>
```

#### Middleware
```ts
// middleware/auth.ts
export default defineNuxtRouteMiddleware((to, from) => {
  const user = useUser()
  if (!user.value && to.path !== '/login') {
    return navigateTo('/login')
  }
})
```

### 🔧 Configuration

#### Nuxt Config
```ts
// nuxt.config.ts
export default defineNuxtConfig({
  app: {
    head: {
      title: 'My Nuxt App',
      meta: [
        { name: 'description', content: 'My amazing Nuxt application' }
      ]
    }
  },
  modules: [
    '@nuxtjs/tailwindcss',
    '@pinia/nuxt'
  ],
  css: ['~/assets/css/main.css'],
  runtimeConfig: {
    public: {
      apiBase: process.env.API_BASE
    }
  }
})
```

## 🚦 Common Use Cases

### Authentication
```vue
<script setup>
const user = useUser()
const { login, logout } = useAuth()

const handleLogin = async () => {
  await login()
  navigateTo('/dashboard')
}
</script>
```

### API Calls
```vue
<script setup>
const { $fetch } = useNuxtApp()

const fetchData = async () => {
  try {
    const data = await $fetch('/api/endpoint')
    // Handle success
  } catch (error) {
    // Handle error
  }
}
</script>
```

## 📦 Deployment

```bash
# Build for production
npm run build

# Preview production build
npm run preview

# Static site generation
npm run generate
```

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## 📝 License

[MIT License](LICENSE)

## 🔗 Links

- [Demo](https://nuxt3-cheatsheet-demo.netlify.app)
- [Documentation](https://nuxt.com/docs)
- [Vue 3 Documentation](https://vuejs.org/)