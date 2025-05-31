<template>
    <div class="relative">
        <!-- Botão Anterior -->
        <button @click="previousPage"
            class="absolute left-0 top-1/2 -translate-y-1/2 -translate-x-5 bg-white p-2 rounded-full shadow-lg hover:bg-gray-100 z-10"
            :disabled="currentPage === 0" :class="{ 'opacity-50 cursor-not-allowed': currentPage === 0 }">
            <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24"
                stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7" />
            </svg>
        </button>

        <!-- Produtos -->
        <div v-if="loading" class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-5 gap-6">
            <div v-for="n in 5" :key="n"
                class="bg-white rounded-xl shadow-md overflow-hidden hover:-translate-y-1 hover:shadow-xl transition-all">
                <div class="aspect-square bg-gray-200 animate-pulse"></div>
                <div class="p-4">
                    <div class="h-4 bg-gray-200 rounded animate-pulse"></div>
                </div>
            </div>
        </div>

        <div v-else-if="error" class="text-center text-red-600">
            <p>{{ error }}</p>
        </div>

        <div v-else class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-5 gap-6">
            <div v-for="product in displayedProducts" :key="product.id"
                class="bg-white rounded-xl shadow-md overflow-hidden hover:-translate-y-1 hover:shadow-xl transition-all">
                <div class="aspect-square">
                    <img :src="product.thumbnail" :alt="product.title" class="w-full h-full object-cover">
                </div>
                <div class="p-4">
                    <h3 class="font-semibold text-neutral-800 text-center line-clamp-2">
                        {{ product.title }}
                    </h3>
                    <p class="text-green-600 font-bold text-center mt-2">
                        ${{ product.price }}
                    </p>
                </div>
            </div>
        </div>

        <!-- Botão Próximo -->
        <button @click="nextPage"
            class="absolute right-0 top-1/2 -translate-y-1/2 translate-x-5 bg-white p-2 rounded-full shadow-lg hover:bg-gray-100 z-10"
            :disabled="currentPage >= Math.ceil(products.length / itemsPerPage) - 1"
            :class="{ 'opacity-50 cursor-not-allowed': currentPage >= Math.ceil(products.length / itemsPerPage) - 1 }">
            <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24"
                stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7" />
            </svg>
        </button>
    </div>
</template>

<script setup>
import { ref, onMounted, computed } from 'vue';
import axios from 'axios';

const products = ref([]);
const loading = ref(true);
const error = ref(null);
const currentPage = ref(0);
const itemsPerPage = 5;

const displayedProducts = computed(() => {
    const start = currentPage.value * itemsPerPage;
    const end = start + itemsPerPage;
    return products.value.slice(start, end);
});

const nextPage = () => {
    if (currentPage.value < Math.ceil(products.value.length / itemsPerPage) - 1) {
        currentPage.value++;
    }
};

const previousPage = () => {
    if (currentPage.value > 0) {
        currentPage.value--;
    }
};

const fetchProducts = async () => {
    try {
        loading.value = true;
        error.value = null;
        const response = await axios.get('https://dummyjson.com/products?limit=20');
        if (response.data && response.data.products) {
            products.value = response.data.products;
        } else {
            error.value = 'Dados dos produtos não encontrados';
        }
    } catch (err) {
        console.error('Erro ao buscar produtos:', err);
        error.value = 'Erro ao carregar os produtos. Tente novamente mais tarde.';
    } finally {
        loading.value = false;
    }
};

onMounted(() => {
    fetchProducts();
});
</script>
