<template>
  <div class="relative">
    <h2 class="text-2xl font-extrabold text-[#4FACFE] text-center mb-8">{{ title }}</h2>

    <div class="relative overflow-x-auto">
      <!-- Loading -->
      <div v-if="loading" class="flex gap-4 pb-4">
        <div v-for="n in 8" :key="n" class="flex-shrink-0 w-64 animate-pulse">
          <div class="bg-gray-200 aspect-square rounded-xl"></div>
          <div class="p-4">
            <div class="h-4 bg-gray-200 rounded w-3/4 mx-auto"></div>
          </div>
        </div>
      </div>

      <!-- Produtos -->
      <div v-else class="flex gap-4 pb-4">
        <router-link v-for="product in visibleProducts" :key="product.id" :to="`/produtos/item/${product.id}`"
          class="flex-shrink-0 w-64 bg-[#F8F8F8] rounded-2xl shadow-lg overflow-hidden hover:-translate-y-1 hover:shadow-xl transition-all duration-200">
          <div class="aspect-square overflow-hidden">
            <img :src="product.thumbnail" :alt="product.title"
              class="w-full h-full object-cover rounded-xl hover:scale-105 transition-transform">
          </div>
          <div class="p-4">
            <h3 class="font-semibold text-neutral-800 text-center line-clamp-2">{{ product.title }}</h3>
            <p class="text-[#4FACFE] font-bold text-center mt-2 text-lg">${{ product.price }}</p>
            <p v-if="showDiscount && product.discountPercentage" class="text-orange-500 text-sm text-center font-bold">
              {{ Math.round(product.discountPercentage) }}% OFF
            </p>
          </div>
        </router-link>
      </div>

      <!-- botões de navegação -->
      <button @click="prevPage"
        class="absolute left-0 top-1/2 -translate-y-1/2 bg-white/90 border-2 border-[#4FACFE] text-[#4FACFE] p-2 rounded-full shadow-lg hover:bg-[#4FACFE] hover:text-white transition-colors z-10">
        <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7" />
        </svg>
      </button>

      <button @click="nextPage"
        class="absolute right-0 top-1/2 -translate-y-1/2 bg-white/90 border-2 border-[#4FACFE] text-[#4FACFE] p-2 rounded-full shadow-lg hover:bg-[#4FACFE] hover:text-white transition-colors z-10">
        <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7" />
        </svg>
      </button>
    </div>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  props: {
    title: String,
    apiUrl: String,
    showDiscount: Boolean
  },
  data() {
    return {
      products: [],
      loading: true,
      currentPage: 0,
      itemsPerPage: 8
    }
  },
  computed: {
    visibleProducts() {
      const start = this.currentPage * this.itemsPerPage
      return this.products.slice(start, start + this.itemsPerPage)
    }
  },
  methods: {
    nextPage() {
      if ((this.currentPage + 1) * this.itemsPerPage < this.products.length) {
        this.currentPage++
      }
    },
    prevPage() {
      if (this.currentPage > 0) {
        this.currentPage--
      }
    },
    async getProducts() {
      try {
        const response = await axios.get(this.apiUrl)
        this.products = response.data.products
      } catch (error) {
        console.error('Erro ao carregar produtos:', error)
      } finally {
        this.loading = false
      }
    }
  },
  mounted() {
    this.getProducts()
  }
}
</script>

<style scoped>
.overflow-x-auto {
  scrollbar-width: none;
  -ms-overflow-style: none;
}

.overflow-x-auto::-webkit-scrollbar {
  display: none;
}
</style>
