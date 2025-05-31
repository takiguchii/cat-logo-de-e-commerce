<template>
  <div class="fixed top-0 left-0 w-64 h-full rounded-r-2xl bg-neutral-900 text-white z-50 shadow-lg">
    <div class="p-6 text-xl font-bold border-b border-neutral-800">
      TechMart
    </div>
    <nav class="p-4 space-y-3">
      <RouterLink to="/" class="block py-2 px-4 rounded hover:bg-neutral-700">início</RouterLink>
      <RouterLink to="/produtos" class="block py-2 px-4 rounded hover:bg-neutral-700">Produtos</RouterLink>
      <RouterLink to="/categorias" class="block py-2 px-4 rounded hover:bg-neutral-700">Categorias ></RouterLink>
      <RouterLink to="/contato" class="block py-2 px-4 rounded hover:bg-neutral-700">Contato</RouterLink>
    </nav>
  </div>
</template>

<script setup>
import { RouterLink } from 'vue-router'
</script>
