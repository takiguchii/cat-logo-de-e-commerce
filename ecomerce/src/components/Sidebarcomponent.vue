<template>
  <div class="fixed top-0 left-0 w-64 h-full bg-[#080C1C] text-[#F8F8F8] z-50 shadow-lg">
    <!-- Header -->
    <div class="p-6 bg-gradient-to-r from-[#4FACFE] to-[#8CE7FE] text-white">
      <h1 class="text-xl font-bold">TechMart</h1>
    </div>

    <!-- Navigation Menu -->
    <nav class="p-4 space-y-3">
      <RouterLink to="/" class="block py-2 px-4 rounded hover:bg-[#4FACFE]/10 transition-colors">
        Início
      </RouterLink>

      <RouterLink to="/produtos" class="block py-2 px-4 rounded hover:bg-[#4FACFE]/10 transition-colors">
        Produtos
      </RouterLink>

      <!-- Categoria com submenu -->
      <div>
        <button @click="submenuAberto = !submenuAberto"
          class="flex items-center w-full py-2 px-4 rounded hover:bg-[#4FACFE]/10 transition-colors">
          <span>Categorias</span>
          <svg :class="{ 'rotate-90': submenuAberto }" class="w-4 h-4 ml-auto transition-transform" fill="none"
            viewBox="0 0 24 24" stroke="currentColor">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7" />
          </svg>
        </button>

        <div v-if="submenuAberto" class="ml-4 mt-2 space-y-1 border-l-2 border-[#4FACFE]/30">
          <RouterLink v-for="category in categories" :key="category" :to="`/produtos/${category}`"
            class="block py-2 px-4 text-sm rounded hover:bg-[#4FACFE]/10 transition-colors border-l-2 border-transparent hover:border-[#4FACFE]">
            {{ formatCategoryName(category) }}
          </RouterLink>
        </div>
      </div>

      <RouterLink to="/contato" class="block py-2 px-4 rounded hover:bg-[#4FACFE]/10 transition-colors">
        Contato
      </RouterLink>
    </nav>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import { RouterLink } from 'vue-router'

const submenuAberto = ref(false)

const categories = [
  'smartphones',
  'laptops',
  'fragrances',
  'groceries',
  'home-decoration',
  'furniture',
  'tops',
  'womens-dresses',
  'womens-shoes',
  'mens-shirts',
  'mens-shoes',
  'mens-watches',
  'womens-watches',
  'womens-bags',
  'womens-jewellery',
  'sunglasses',
  'motorcycle'
]

const formatCategoryName = (category) => {
  return category
    .split('-')
    .map(word => word.charAt(0).toUpperCase() + word.slice(1))
    .join(' ')
}
</script>

