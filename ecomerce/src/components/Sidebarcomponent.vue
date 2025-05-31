<template>
  <div class="fixed top-0 left-0 w-64 h-full rounded-r-2xl bg-neutral-900 text-white z-50 shadow-lg">
    <div class="p-6 text-xl font-bold border-b border-neutral-800">
      TechMart
    </div>
    <nav class="p-4 space-y-3">
      <RouterLink to="/" class="block py-2 px-4 rounded hover:bg-neutral-700">Início</RouterLink>
      <RouterLink to="/produtos" class="block py-2 px-4 rounded hover:bg-neutral-700">Produtos</RouterLink>

      <!-- Categoria com submenu -->
      <div>
        <button
          @click="submenuAberto = !submenuAberto"
          class="flex items-center w-full py-2 px-4 rounded hover:bg-neutral-700 transition group"
        >
          Categorias
          <svg :class="{'rotate-90': submenuAberto}" class="w-4 h-4 ml-auto transition-transform" fill="none" viewBox="0 0 24 24" stroke="currentColor">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7"/>
          </svg>
        </button>
        <div v-if="submenuAberto" class="ml-4 mt-2 space-y-2 transition">
          <RouterLink to="/categorias/eletronicos" class="block py-1 px-2 rounded hover:bg-neutral-700 text-sm">Eletrônicos</RouterLink>
          <RouterLink to="/categorias/acessorios" class="block py-1 px-2 rounded hover:bg-neutral-700 text-sm">Acessórios</RouterLink>
          <RouterLink to="/categorias/games" class="block py-1 px-2 rounded hover:bg-neutral-700 text-sm">Games</RouterLink>
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
</script>
