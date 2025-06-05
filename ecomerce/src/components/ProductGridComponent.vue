<template>
  <div class="container mx-auto p-6">
    <!-- Carrega pagina -->
    <div v-if="loading" class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4 xl:grid-cols-5 gap-6">
      <div v-for="n in 20" :key="n" class="animate-pulse">
        <div class="bg-gray-200 aspect-square rounded-2xl"></div>
        <div class="mt-4 space-y-3">
          <div class="h-4 bg-gray-200 rounded w-3/4"></div>
          <div class="h-4 bg-gray-200 rounded w-1/2"></div>
        </div>
      </div>
    </div>

    <!-- Verifica erros  -->
    <div v-else-if="error" class="text-center text-red-600 py-10">
      {{ error }}
    </div>

    <!-- Product grid -->
    <div v-else>
      <div class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4 xl:grid-cols-5 gap-6">
        <router-link v-for="product in productsToShow" :key="product.id" :to="`/produtos/item/${product.id}`"
          class="bg-[#F8F8F8] rounded-2xl shadow-lg overflow-hidden transition-all duration-200 hover:shadow-2xl hover:-translate-y-1 block">
          <div class="aspect-square overflow-hidden">
            <img :src="product.thumbnail" :alt="product.title"
              class="w-full h-full object-cover rounded-xl transition-transform duration-200 hover:scale-105" />
          </div>

          <div class="p-4">
            <div class="text-xs text-[#4FACFE] mb-1 capitalize font-semibold">{{ product.category }}</div>
            <h3 class="font-semibold text-neutral-800 mb-2 text-center line-clamp-2">{{ product.title }}</h3>
            <div class="space-y-2">
              <div class="text-lg font-bold text-[#4FACFE] text-center">${{ product.price }}</div>
              <div class="text-xs text-center">
                <span :class="product.stock > 0 ? 'text-green-500' : 'text-red-500'" class="font-bold">
                  {{ product.stock > 0 ? `${product.stock} disponíveis` : 'Fora de estoque' }}
                </span>
              </div>
            </div>
          </div>
        </router-link>
      </div>

      <!-- Paginação -->
      <div class="mt-8 flex justify-center gap-4">
        <button @click="page = page - 1" :disabled="page === 1"
          class="px-4 py-2 bg-[#4FACFE] text-white rounded-xl font-semibold shadow hover:bg-[#8CE7FE] transition-colors disabled:opacity-50 disabled:cursor-not-allowed">
          Anterior
        </button>
        <span class="px-4 py-2 bg-white rounded-xl font-semibold shadow text-[#080C1C]">
          Página {{ page }} de {{ totalPages }}
        </span>
        <button @click="page = page + 1" :disabled="page === totalPages"
          class="px-4 py-2 bg-[#4FACFE] text-white rounded-xl font-semibold shadow hover:bg-[#8CE7FE] transition-colors disabled:opacity-50 disabled:cursor-not-allowed">
          Próxima
        </button>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  props: {
    category: String
  },
  data() {
    return {
      products: [],
      loading: true,
      error: null,
      page: 1,
      productsPerPage: 20
    }
  },
  computed: {
    totalPages() {
      return Math.ceil(this.products.length / this.productsPerPage)
    },
    productsToShow() {
      const start = (this.page - 1) * this.productsPerPage
      const end = start + this.productsPerPage
      return this.products.slice(start, end)
    }
  },
  watch: {
    category: {
      handler: 'loadProducts',
      immediate: true
    }
  },
  methods: {
    async loadProducts() {
      this.loading = true
      this.error = null
      this.page = 1

      try {
        const url = this.category
          ? `https://dummyjson.com/products/category/${this.category}`
          : 'https://dummyjson.com/products?limit=100'

        const response = await axios.get(url)
        this.products = response.data.products
      } catch (err) {
        console.error('Erro:', err)
        this.error = 'Erro ao carregar os produtos. Tente novamente.'
      } finally {
        this.loading = false
      }
    }
  }
}
</script>
