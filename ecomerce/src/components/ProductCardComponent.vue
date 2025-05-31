<template>
    <div class="relative">
        <h2 class="text-2xl font-bold text-neutral-800 text-center mb-8">{{ title }}</h2>

        <!-- Container -->
        <div class="relative overflow-x-auto">
            <!-- Carregando estado -->
            <div v-if="loading" class="flex gap-4 pb-4">
                <div v-for="n in 8" :key="n" class="flex-shrink-0 w-64 animate-pulse">
                    <div class="bg-gray-200 aspect-square rounded-xl"></div>
                    <div class="p-4">
                        <div class="h-4 bg-gray-200 rounded w-3/4 mx-auto"></div>
                    </div>
                </div>
            </div>

            <!-- lista de produtos -->
            <div v-else class="flex gap-4 pb-4">
                <div v-for="product in productsToShow" :key="product.id"
                    class="flex-shrink-0 w-64 bg-white rounded-xl shadow-md overflow-hidden hover:-translate-y-1 hover:shadow-xl transition-all">
                    <div class="aspect-square">
                        <img :src="product.thumbnail" :alt="product.title" class="w-full h-full object-cover">
                    </div>
                    <div class="p-4">
                        <h3 class="font-semibold text-neutral-800 text-center line-clamp-2">{{ product.title }}</h3>
                        <p class="text-green-600 font-bold text-center mt-2">${{ product.price }}</p>
                        <p v-if="showDiscount && product.discountPercentage" class="text-red-500 text-sm text-center">
                            {{ Math.round(product.discountPercentage) }}% OFF
                        </p>
                    </div>
                </div>
            </div>

            <!-- botão de nnavegação -->
            <button @click="prevPage" class="absolute left-0 top-1/2 -translate-y-1/2 bg-white/80 p-2 rounded-full shadow-lg hover:bg-white z-10"
                :style="{ opacity: page === 0 ? 0.5 : 1 }">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7" />
                </svg>
            </button>

            <button @click="nextPage" class="absolute right-0 top-1/2 -translate-y-1/2 bg-white/80 p-2 rounded-full shadow-lg hover:bg-white z-10"
                :style="{ opacity: !hasMorePages ? 0.5 : 1 }">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7" />
                </svg>
            </button>
        </div>
    </div>
</template>

<script>
export default {
    props: {
        title: String,
        apiUrl: String,
        showDiscount: {
            type: Boolean,
            default: false
        }
    },

    data() {
        return {
            products: [],
            loading: true,
            page: 0,
            productsPerPage: 8
        }
    },

    computed: {
        productsToShow() {
            const start = this.page * this.productsPerPage
            const end = start + this.productsPerPage
            return this.products.slice(start, end)
        },
        hasMorePages() {
            return this.page < Math.floor(this.products.length / this.productsPerPage)
        }
    },

    methods: {
        nextPage() {
            if (this.hasMorePages) {
                this.page++
            }
        },
        prevPage() {
            if (this.page > 0) {
                this.page--
            }
        },
        async loadProducts() {
            try {
                this.loading = true
                const response = await fetch(this.apiUrl)
                const data = await response.json()
                this.products = data.products
            } catch (error) {
                console.error('Error loading products:', error)
            } finally {
                this.loading = false
            }
        }
    },

    mounted() {
        this.loadProducts()
    }
}
</script>

<style scoped>
.overflow-x-auto {
    -webkit-overflow-scrolling: touch;
    scrollbar-width: none;
    -ms-overflow-style: none;
}

.overflow-x-auto::-webkit-scrollbar {
    display: none;
}
</style>
