<script setup>
import { computed } from 'vue'
import { useRoute } from 'vue-router'
import ProductGridComponent from '../components/ProductGridComponent.vue'

const route = useRoute()

const categoryTitle = computed(() => {
    const category = route.params.category
    return category
        ? category.split('-').map(word => word.charAt(0).toUpperCase() + word.slice(1)).join(' ')
        : 'Todos os Produtos'
})
</script>

<template>
    <div class="min-h-screen bg-gray-100 py-10 px-4">
        <div class="max-w-7xl mx-auto">
            <h1 class="text-3xl font-bold text-gray-800 mb-8 text-center capitalize">
                {{ categoryTitle }}
            </h1>
            <ProductGridComponent :key="$route.params.category" :category="$route.params.category" />
        </div>
    </div>
</template>
