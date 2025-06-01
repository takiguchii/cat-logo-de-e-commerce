<template>
  <nav class="bg-[#080C1C] p-4 shadow-lg">
    <div class="container mx-auto flex justify-between items-center">
      <!-- Botão Sidebar -->
      <button @click="$emit('toggle-sidebar')"
        class="text-[#F8F8F8] hover:text-[#4FACFE] transition-colors duration-200">
        <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16M4 18h16" />
        </svg>
      </button>

      <!-- Barra de Pesquisa -->
      <div class="flex-1 mx-4">
        <div class="relative max-w-xl mx-auto">
          <input type="text" placeholder="Digite aqui..." class="w-full px-4 py-2 rounded-lg bg-[#080C1C] border border-[#4FACFE]/30 
                   text-[#F8F8F8] placeholder-[#F8F8F8]/50
                   focus:outline-none focus:border-[#4FACFE] focus:ring-1 focus:ring-[#4FACFE]
                   transition-all duration-200" />
        </div>
      </div>

      <!-- Marca -->
      <RouterLink to="/" class="bg-gradient-to-r from-[#4FACFE] to-[#8CE7FE] bg-clip-text text-transparent 
               font-bold text-xl hover:opacity-80 transition-opacity duration-200">
        TechMart
      </RouterLink>
    </div>
  </nav>
</template>

<script setup>
import { RouterLink } from 'vue-router'
defineEmits(['toggle-sidebar'])
</script>
