<template>
  <div class="fixed top-0 left-0 w-64 h-full rounded-r-2xl bg-neutral-900 text-white z-50 shadow-lg overflow-y-auto">
    <div class="p-6 text-xl font-bold border-b border-neutral-800">
      TechMart
    </div>
    <nav class="p-4 space-y-3">
      <RouterLink to="/" class="block py-2 px-4 rounded hover:bg-neutral-700">Início</RouterLink>
      <RouterLink to="/produtos" class="block py-2 px-4 rounded hover:bg-neutral-700">Produtos</RouterLink>

      <!-- Categoria com submenu -->
      <div>
        <button @click="submenuAberto = !submenuAberto"
          class="flex items-center w-full py-2 px-4 rounded hover:bg-neutral-700 transition group">
          <span>Categorias</span>
          <svg :class="{ 'rotate-90': submenuAberto }" class="w-4 h-4 ml-auto transition-transform" fill="none"
            viewBox="0 0 24 24" stroke="currentColor">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7" />
          </svg>
        </button>

        <div v-if="submenuAberto" class="ml-4 mt-2 space-y-1 max-h-[60vh] overflow-y-auto">
          <RouterLink v-for="category in categories" :key="category" :to="`/produtos/${category}`"
            class="block py-2 px-4 text-sm rounded hover:bg-neutral-700 capitalize transition-colors">
            {{ formatCategoryName(category) }}
          </RouterLink>
        </div>
      </div>

      <RouterLink to="/contato" class="block py-2 px-4 rounded hover:bg-neutral-700">Contato</RouterLink>
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

<style scoped>
.overflow-y-auto {
  scrollbar-width: thin;
  scrollbar-color: #4B5563 #1F2937;
}

.overflow-y-auto::-webkit-scrollbar {
  width: 6px;
}

.overflow-y-auto::-webkit-scrollbar-track {
  background: #1F2937;
}

.overflow-y-auto::-webkit-scrollbar-thumb {
  background-color: #4B5563;
  border-radius: 3px;
}
</style>
