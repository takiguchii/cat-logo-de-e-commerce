<template>
  <nav class="bg-gray-800 p-4">
    <div class="container mx-auto flex justify-between items-center">
      <RouterLink to="/" class="text-white font-bold text-xl">E-commerce</RouterLink>
      <div class="space-x-4">
        <RouterLink to="/" class="text-white hover:text-gray-300">Home</RouterLink>
        <RouterLink to="/about" class="text-white hover:text-gray-300">About</RouterLink>
      </div>
    </div>
  </nav>
</template>

<script setup>
import { RouterLink } from 'vue-router'
</script>
