<template>
  <div class="max-w-4xl mx-auto p-8 mt-10 bg-white rounded-3xl shadow-lg min-h-[400px]">
    <div v-if="loading" class="text-center text-neutral-400">Carregando...</div>
    <div v-else-if="error" class="text-center text-red-500">{{ error }}</div>
    <div v-else>
      <div class="flex flex-col md:flex-row gap-8 items-center md:items-start">
        <!-- imagens do produto -->
        <div class="flex-shrink-0">
          <!-- Imagem principal  -->
          <img v-if="product.thumbnail" :src="product.thumbnail" :alt="product.title"
            class="w-72 h-72 object-cover rounded-xl shadow mb-6 md:mb-0" />
          <!-- imagens secundárias -->
          <div class="flex gap-2 mt-4">
            <img v-for="image in product.images?.slice(0, 3)" :key="image" :src="image"
              class="w-20 h-20 object-cover rounded-lg cursor-pointer hover:opacity-75" />
          </div>
        </div>

        <!-- detalhes do produto -->
        <div class="flex-1 w-full">
          <h1 class="text-3xl font-bold mb-4 text-neutral-900">{{ product.title }}</h1>

          <!-- Sistema de avaliação-->
          <div class="flex items-center mb-4">
            <div class="flex text-yellow-400">
              <span v-for="i in Math.floor(product.rating)" :key="i">★</span>
              <!--Nunca demorei tanto pra achar um emoji-->
              <span class="text-gray-300">{{ '★'.repeat(5 - Math.floor(product.rating)) }}</span>
            </div>
            <span class="ml-2 text-neutral-600">({{ product.rating }})</span>
          </div>

          <!-- Preço e desconto -->
          <div class="mb-6">
            <span class="text-3xl font-bold text-neutral-900">${{ product.price }}</span>
            <span class="ml-2 text-sm text-green-600" v-if="product.discountPercentage">
              {{ product.discountPercentage }}% OFF
            </span>
          </div>

          <!-- Informações adicionais do produto -->
          <div class="space-y-4 mb-6">
          </div>

          <!-- Descrição do produto -->
          <div class="mt-8">
            <h2 class="text-xl font-semibold mb-2 text-neutral-800">Descrição</h2>
            <p class="text-neutral-600">{{ product.description }}</p>
          </div>
            <!-- Seção de avaliações dos clientes -->
            <div class="mt-12">
              <h2 class="text-xl font-semibold mb-4 text-neutral-800">Avaliações dos Clientes</h2>
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
                    <span class="ml-2 font-medium text-neutral-800">{{ review.reviewerName }}</span>
                    <span class="ml-2 text-sm text-neutral-500">{{ new Date(review.date).toLocaleDateString() }}</span>
                  </div>
                  <p class="text-neutral-600">{{ review.comment }}</p>
                </div>
              </div>
            </div>

          <router-link to="/"
            class="inline-flex items-center mt-8 px-4 py-2 bg-blue-600 text-white rounded-lg hover:bg-blue-700 transition-colors">
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
