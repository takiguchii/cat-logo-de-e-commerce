<template>
    <div class="bg-white rounded-xl shadow-lg p-6">
        <!-- Carregando estado  -->
        <div v-if="loading" class="grid grid-cols-5 gap-6">
            <div v-for="n in 20" :key="n" class="animate-pulse">
                <div class="bg-gray-200 aspect-square rounded-lg"></div>
                <div class="mt-4 space-y-3">
                    <div class="h-4 bg-gray-200 rounded w-3/4"></div>
                    <div class="h-4 bg-gray-200 rounded w-1/2"></div>
                </div>
            </div>
        </div>

        <!-- Produtos da grid  -->
        <div v-else>
            <div class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-5 gap-6">
                <div v-for="product in paginatedProducts" :key="product.id"
                    class="bg-white rounded-xl shadow-md overflow-hidden hover:-translate-y-1 hover:shadow-xl transition-all">
                    <div class="aspect-square">
                        <img :src="product.thumbnail" :alt="product.title" class="w-full h-full object-cover">
                    </div>
                    <div class="p-4">
                        <h3 class="font-semibold text-neutral-800 text-center line-clamp-2">{{ product.title }}</h3>
                        <p class="text-green-600 font-bold text-center mt-2">${{ product.price }}</p>
                    </div>
                </div>
            </div>

            <!-- Paginação -->
            <div class="mt-8 flex justify-center gap-4">
                <button @click="prevPage" :disabled="currentPage === 1"
                    class="px-4 py-2 bg-gray-800 text-white rounded-lg disabled:opacity-50 disabled:cursor-not-allowed">
                    Anterior
                </button>

                <button @click="nextPage" :disabled="currentPage === totalPages"
                    class="px-4 py-2 bg-gray-800 text-white rounded-lg disabled:opacity-50 disabled:cursor-not-allowed">
                    Próxima
                </button>
            </div>
        </div>
    </div>
</template>

<script setup>
import { ref, computed, onMounted } from 'vue'

const products = ref([])
const loading = ref(true)
const currentPage = ref(1)
const productsPerPage = 20

const totalPages = computed(() => Math.ceil(products.value.length / productsPerPage))

const paginatedProducts = computed(() => {
    const start = (currentPage.value - 1) * productsPerPage
    const end = start + productsPerPage
    return products.value.slice(start, end)
})

const nextPage = () => {
    if (currentPage.value < totalPages.value) {
        currentPage.value++
        window.scrollTo({ top: 0, behavior: 'smooth' })
    }
}

const prevPage = () => {
    if (currentPage.value > 1) {
        currentPage.value--
        window.scrollTo({ top: 0, behavior: 'smooth' })
    }
}

onMounted(async () => {
    try {
        const response = await fetch('https://dummyjson.com/products?limit=100')
        const data = await response.json()
        products.value = data.products
    } catch (error) {
        console.error('Error fetching products:', error)
    } finally {
        loading.value = false
    }
})
</script>
