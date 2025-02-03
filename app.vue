<template>
  <div class="p-8 max-w-4xl mx-auto">
    <h1 class="text-4xl font-bold mb-8">Nuxt 3 Cheatsheet</h1>
    
    <section class="mb-8">
      <h2 class="text-2xl font-semibold mb-4">1. Project Structure</h2>
      <pre class="bg-gray-100 p-4 rounded">
/
├── .nuxt/          # Auto-generated build directory
├── app.vue         # Main app template
├── assets/         # Uncompiled assets (scss, images)
├── components/     # Vue components (auto-imported)
├── composables/    # Composable functions (auto-imported)
├── content/        # Content files for Nuxt Content
├── layouts/        # Layout components
├── middleware/     # Navigation middleware
├── pages/          # Application pages (auto-routed)
├── plugins/        # Vue plugins
├── public/         # Static files (directly served)
├── server/         # Server routes and middleware
└── nuxt.config.ts  # Nuxt configuration file</pre>
    </section>

    <section class="mb-8">
      <h2 class="text-2xl font-semibold mb-4">2. Key Features</h2>
      <ul class="list-disc pl-6 space-y-2">
        <li>Auto-imports for components and composables</li>
        <li>File-based routing</li>
        <li>Server-side rendering (SSR)</li>
        <li>Static site generation (SSG)</li>
        <li>Hybrid rendering modes</li>
        <li>Vue 3 and Composition API</li>
        <li>TypeScript support</li>
        <li>Hot module replacement</li>
      </ul>
    </section>

    <section class="mb-8">
      <h2 class="text-2xl font-semibold mb-4">3. Common Patterns</h2>
      
      <div class="mb-4">
        <h3 class="text-xl font-medium mb-2">Data Fetching</h3>
        <pre class="bg-gray-100 p-4 rounded">
// Composable
const { data } = await useFetch('/api/users')

// Component
const { data: posts } = await useLazyFetch('/api/posts')

// Server route
export default defineEventHandler(async (event) => {
  return { message: 'Hello from API' }
})
<hr class="mt-5"/>
// Dont Initial HTML , Dont Fetch On Initial Client Load
const {data, execute} = await useAsyncData(()=>{/*...*/} , {immediate: false})
//later on
execute()
<hr class="mt-5"/>
//Dont Initial HTML , But Fetch On Initial Client Load (Block Client Side Nav)
const {data } = await useAsyncData(()=> /*...*/ , {server: false})
<hr class="mt-5"/>
// Initial on HTML , Don't Block During Client Navigation
const {data,pending} = await useAsyncData(()=>/*...*/ , {lazy:true})
<hr class="mt-5"/>
//Initial on HTML ,Block During Client Navigation (Block Client Side Nav)
const {data} = await useAsyncData (() => /*...*/, {//Other Options})

</pre>
      </div>

      <div class="mb-4">
        <h3 class="text-xl font-medium mb-2">State Management</h3>
        <pre class="bg-gray-100 p-4 rounded">
// composables/useState.ts
export const useCounter = () => useState('counter', () => 0)

// Component usage
const counter = useCounter()
counter.value++</pre>
      </div>

      <div class="mb-4">
        <h3 class="text-xl font-medium mb-2">Middleware</h3>
        <pre class="bg-gray-100 p-4 rounded">
// middleware/auth.ts
export default defineNuxtRouteMiddleware((to, from) => {
  const user = useUser()
  if (!user.value) return navigateTo('/login')
})</pre>
      </div>
    </section>

    <section class="mb-8">
      <h2 class="text-2xl font-semibold mb-4">4. Configuration</h2>
      <pre class="bg-gray-100 p-4 rounded">
// nuxt.config.ts
export default defineNuxtConfig({
  // App config
  app: {
    head: {
      title: 'My Nuxt App'
    }
  },
  
  // Modules
  modules: [
    '@nuxtjs/tailwindcss',
    '@pinia/nuxt'
  ],
  
  // Runtime config
  runtimeConfig: {
    apiSecret: '', // server-only
    public: {
      apiBase: '' // client & server
    }
  },
  
  // Build options
  build: {
    transpile: []
  }
})</pre>
    </section>

    <section class="mb-8">
      <h2 class="text-2xl font-semibold mb-4">5. Deployment Commands</h2>
      <pre class="bg-gray-100 p-4 rounded">
# Development
npm run dev

# Production build
npm run build

# Static site generation
npm run generate

# Preview production build
npm run preview</pre>
    </section>
  </div>
</template>

<style>
body {
  font-family: system-ui, -apple-system, sans-serif;
  line-height: 1.5;
  color: #374151;
}

pre {
  overflow-x: auto;
  white-space: pre-wrap;
  word-wrap: break-word;
}
</style>