<template>
  <div class="max-w-4xl mx-auto p-8 mt-10 bg-[#F8F8F8] rounded-3xl shadow-xl min-h-[400px]">
    <div v-if="loading" class="text-center text-[#4FACFE]">Carregando...</div>
    <div v-else-if="error" class="text-center text-red-500">{{ error }}</div>
    <div v-else>
      <div class="flex flex-col md:flex-row gap-10 items-center md:items-start">
        <!-- imagens do produto -->
        <div class="flex-shrink-0">
          <!-- Imagem principal -->
          <img v-if="product.thumbnail" :src="product.thumbnail" :alt="product.title"
            class="w-72 h-72 object-cover rounded-2xl shadow-lg mb-6 md:mb-0" />
          <!-- imagens secundárias -->
          <div class="flex gap-2 mt-4">
            <img v-for="image in product.images?.slice(0, 3)" :key="image" :src="image"
              class="w-20 h-20 object-cover rounded-lg cursor-pointer hover:opacity-75 border border-[#4FACFE]/30 transition" />
          </div>
        </div>

        <!-- detalhes do produto -->
        <div class="flex-1 w-full">
          <h1 class="text-3xl font-extrabold mb-4 text-[#080C1C] tracking-wide">{{ product.title }}</h1>

          <!-- Sistema de avaliação-->
          <div class="flex items-center mb-4">
            <div class="flex text-yellow-400">
              <span v-for="i in Math.floor(product.rating)" :key="i">★</span>
              <span class="text-gray-300">{{ '★'.repeat(5 - Math.floor(product.rating)) }}</span>
            </div>
            <span class="ml-2 text-neutral-600">({{ product.rating }})</span>
          </div>

          <!-- Preço e desconto -->
          <div class="mb-6 flex flex-col sm:flex-row sm:items-end gap-2">
            <span class="text-3xl font-bold text-[#4FACFE]">${{ product.price }}</span>
            <span class="ml-2 text-sm text-green-600 font-bold" v-if="product.discountPercentage">
              {{ product.discountPercentage }}% OFF
            </span>
          </div>

          <!-- Descrição do produto -->
          <div class="mt-8">
            <h2 class="text-xl font-semibold mb-2 text-[#4FACFE]">Descrição</h2>
            <p class="text-neutral-700">{{ product.description }}</p>
          </div>
          <!-- Seção de avaliações dos clientes -->
          <div class="mt-12">
            <h2 class="text-xl font-semibold mb-4 text-[#4FACFE]">Avaliações dos Clientes</h2>
            <div v-if="!product.reviews?.length" class="text-neutral-500">
              Ainda não há avaliações para este produto.
            </div>
            <div v-else class="space-y-4">
              <div v-for="review in product.reviews" :key="review.reviewerEmail" class="border-b border-gray-200 pb-4">
                <div class="flex items-center mb-2">
                  <div class="flex text-yellow-400">
                    <span v-for="i in review.rating" :key="i">★</span>
                    <span class="text-gray-300">{{ '★'.repeat(5 - review.rating) }}</span>
                  </div>
                  <span class="ml-2 font-medium text-[#080C1C]">{{ review.reviewerName }}</span>
                  <span class="ml-2 text-sm text-neutral-500">{{ new Date(review.date).toLocaleDateString() }}</span>
                </div>
                <p class="text-neutral-600">{{ review.comment }}</p>
              </div>
            </div>
          </div>

          <router-link to="/produtos"
            class="inline-flex items-center mt-8 px-4 py-2 bg-[#4FACFE] text-white rounded-full font-semibold hover:bg-[#8CE7FE] transition-colors shadow">
            <span class="mr-2">←</span>
            Voltar para Produtos
          </router-link>
        </div>
      </div>
    </div>
  </div>
</template>


<script setup>
import { ref, onMounted } from 'vue'
import { useRoute } from 'vue-router'

const route = useRoute()
const product = ref({})
const loading = ref(true)
const error = ref(null)

// Dados mockados das avaliações
const reviews = ref([
  {
    id: 1,
    rating: 4,
    comment: "Very satisfied!",
    user: "Lucas Gordon",
    date: "2023-11-30"
  }
])

onMounted(async () => {
  try {
    const res = await fetch(`https://dummyjson.com/products/${route.params.id}`)
    if (!res.ok) throw new Error('Produto não encontrado.')
    product.value = await res.json()
  } catch (e) {
    error.value = e.message
  } finally {
    loading.value = false
  }
})
</script>
