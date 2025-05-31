<template>
    <div class="min-h-screen bg-gray-100 py-10 px-4">
        <div class="max-w-7xl mx-auto">
            <h1 class="text-3xl font-bold text-gray-800 mb-8 text-center">Nossos Produtos</h1>
            <ProductGridComponent />
        </div>
    </div>
</template>

<script setup>
import ProductGridComponent from '../components/ProductGridComponent.vue'
</script>
