<script setup lang="ts">
import { RouterLink } from 'vue-router'
import { useCartStore } from '@/stores/cart'
import { useTheme } from '@/composables/useTheme'
import { useAuthStore } from '@/stores/auth'

const cart = useCartStore()
const { theme, toggle } = useTheme()
const auth = useAuthStore()
</script>

<template>
  <header class="text-white" style="background-color: #9D00FF;">
    <div class="max-w-6xl mx-auto px-4 py-3 flex items-center justify-between">
      <RouterLink to="/" class="flex items-center">
  <img src="/logo.png" alt="WLSMart" class="h-14 w-48" />
</RouterLink>

      <nav class="flex items-center gap-4">
  <RouterLink to="/" class="text-white hover:underline">Home</RouterLink>

  <RouterLink to="/cart" class="text-white hover:underline">
    Cart
    <span
      v-if="cart.totalItems > 0"
      class="ml-2 inline-flex items-center justify-center text-xs font-bold px-2 py-1 rounded-full bg-white text-black"
    >
      {{ cart.totalItems }}
    </span>
  </RouterLink>

  <RouterLink v-if="!auth.isLoggedIn" to="/login" class="text-white hover:underline">
    Login
  </RouterLink>

  <button
    v-else
    class="px-3 py-1 rounded border border-white text-white hover:bg-white hover:text-purple-600"
    @click="auth.logout()"
  >
    Logout
  </button>

  <button
    @click="toggle"
    class="relative w-16 h-8 rounded-full border border-white/70 transition-colors duration-300"
    :class="theme === 'dark' ? 'bg-gray-900' : 'bg-white/20'"
    aria-label="Toggle theme"
  >
    <span
      class="absolute top-1 left-1 w-6 h-6 rounded-full flex items-center justify-center text-xs transition-transform duration-300 bg-white text-black"
      :class="theme === 'dark' ? 'translate-x-8' : 'translate-x-0'"
    >
      {{ theme === 'dark' ? '🌙' : '☀️' }}
    </span>
  </button>
</nav>
    </div>
  </header>
</template>