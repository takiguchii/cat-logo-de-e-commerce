<template>
    <div class="container mx-auto p-6">
        <!-- carregando estado -->
        <div v-if="loading" class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4 xl:grid-cols-5 gap-6">
            <div v-for="n in 20" :key="n" class="animate-pulse">
                <div class="bg-gray-200 aspect-square rounded-lg"></div>
                <div class="mt-4 space-y-3">
                    <div class="h-4 bg-gray-200 rounded w-3/4"></div>
                    <div class="h-4 bg-gray-200 rounded w-1/2"></div>
                </div>
            </div>
        </div>

        <!-- Error State -->
        <div v-else-if="error" class="text-center text-red-600 py-10">
            {{ error }}
        </div>

        <!-- Produtos da grid -->
        <div v-else>
            <div class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4 xl:grid-cols-5 gap-6">
                <router-link
                    v-for="product in currentProducts"
                    :key="product.id"
                    :to="{ name: 'ProductDetail', params: { id: product.id } }"
                    class="bg-white rounded-lg shadow-md overflow-hidden hover:shadow-xl transition-shadow duration-300 block"
                >
                    <!-- Imagem do Produto (Sem o badge de estoque) -->
                    <div class="aspect-square">
                        <img :src="product.thumbnail" :alt="product.title" class="w-full h-full object-cover">
                    </div>

                    <!-- Informações do Produto -->
                    <div class="p-4">
                        <div class="text-sm text-gray-500 mb-1 capitalize">{{ product.category }}</div>
                        <h3 class="font-semibold text-gray-800 mb-2 line-clamp-2">{{ product.title }}</h3>

                        <div class="space-y-2">
                            <!-- Preço -->
                            <div class="text-lg font-bold text-green-600">${{ product.price.toFixed(2) }}</div>

                            <!-- Status do Estoque -->
                            <div class="text-sm">
                                <span :class="[
                                    'text-sm',
                                    product.stock > 0 ? 'text-green-600' : 'text-red-500'
                                ]">
                                    {{ product.stock > 0 ? `${product.stock} unidades disponíveis` : 'Fora de estoque'
                                    }}
                                </span>
                            </div>
                        </div>
                    </div>
                </router-link>
            </div>

            <!-- Paginação-->
            <div class="mt-8 flex justify-center gap-4">
                <button @click="prevPage" :disabled="currentPage === 1"
                    class="px-4 py-2 bg-gray-800 text-white rounded-lg disabled:opacity-50 disabled:cursor-not-allowed">
                    Anterior
                </button>
                <span class="px-4 py-2 bg-gray-100 rounded-lg">
                    Página {{ currentPage }} de {{ totalPages }}
                </span>
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
const error = ref(null)
const currentPage = ref(1)
const itemsPerPage = 20

const totalPages = computed(() => Math.ceil(products.value.length / itemsPerPage))
const currentProducts = computed(() => {
    const start = (currentPage.value - 1) * itemsPerPage
    const end = start + itemsPerPage
    return products.value.slice(start, end)
})

const fetchProducts = async () => {
    try {
        loading.value = true
        const response = await fetch('https://dummyjson.com/products?limit=100')
        const data = await response.json()
        if (!data.products) throw new Error('Dados inválidos recebidos da API')
        products.value = data.products
    } catch (err) {
        error.value = 'Erro ao carregar produtos. Por favor, tente novamente.'
        console.error('Erro:', err)
    } finally {
        loading.value = false
    }
}

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

onMounted(() => {
    fetchProducts()
})
</script>
