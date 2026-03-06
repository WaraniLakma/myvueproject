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
  <header class="bg-white border-b dark:bg-gray-900 dark:border-gray-700">
    <div class="max-w-6xl mx-auto px-4 py-3 flex items-center justify-between">
      <RouterLink to="/" class="text-lg font-bold">Vue Store</RouterLink>

      <nav class="flex items-center gap-4">
        <RouterLink to="/" class="hover:underline">Home</RouterLink>

        <RouterLink to="/cart" class="relative hover:underline">
          Cart
          <span
            v-if="cart.totalItems > 0"
            class="ml-2 inline-flex items-center justify-center text-xs font-bold px-2 py-1 rounded-full bg-black text-white"
          >
            {{ cart.totalItems }}
          </span>
        </RouterLink>

        <!-- ✅ Auth: Login / Logout -->
        <RouterLink v-if="!auth.isLoggedIn" to="/login" class="hover:underline">
          Login
        </RouterLink>

        <button
          v-else
          class="px-3 py-1 rounded border hover:bg-gray-100 dark:hover:bg-gray-800"
          @click="auth.logout()"
        >
          Logout
        </button>

        <!-- 🌙 Dark Mode Toggle -->
        <button
          class="px-3 py-1 rounded border hover:bg-gray-100 dark:hover:bg-gray-800"
          @click="toggle"
        >
          {{ theme === 'dark' ? 'Light' : 'Dark' }}
        </button>
      </nav>
    </div>
  </header>
</template>