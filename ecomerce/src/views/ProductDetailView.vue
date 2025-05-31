<template>
  <div class="max-w-2xl mx-auto p-8 mt-10 bg-white rounded-3xl shadow-lg min-h-[400px]">
    <div v-if="loading" class="text-center text-neutral-400">Carregando...</div>
    <div v-else-if="error" class="text-center text-red-500">{{ error }}</div>
    <div v-else>
      <h1 class="text-3xl font-bold mb-4 text-neutral-900">{{ product.title }}</h1>
      <img
        v-if="product.thumbnail"
        :src="product.thumbnail"
        :alt="product.title"
        class="w-56 h-56 object-cover mx-auto mb-6 rounded-xl shadow"
      />
      <p class="text-neutral-700 mb-1">
        <span class="font-semibold">Marca:</span> {{ product.brand }}
      </p>
      <p class="text-neutral-700 mb-1">
        <span class="font-semibold">Categoria:</span> {{ product.category }}
      </p>
      <p class="text-neutral-700 mb-1">
        <span class="font-semibold">Preço:</span> ${{ product.price }}
      </p>
      <p class="text-neutral-700 mb-4">
        <span class="font-semibold">Estoque:</span> {{ product.stock }}
      </p>
      <div>
        <h2 class="text-xl font-semibold mb-2 text-neutral-800">Descrição</h2>
        <p class="text-neutral-600">{{ product.description }}</p>
      </div>
      <router-link
        to="/produtos"
        class="block mt-8 text-blue-600 hover:underline text-center"
      >
        Voltar para Produtos
      </router-link>
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

