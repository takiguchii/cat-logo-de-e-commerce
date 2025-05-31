<template>
  <div class="min-h-screen flex flex-col bg-gray-100">
    <div class="w-full h-[400px] bg-cover bg-center bg-no-repeat"
      style="background-image: url('https://img.freepik.com/fotos-gratis/luminaria-de-neon-para-vendas-de-sexta-feira-negra_23-2151833076.jpg?semt=ais_hybrid&w=740');">
      <div class="h-full flex flex-col justify-center pl-20 text-white bg-black/60">
        <h1 class="text-6xl font-bold mb-4 tracking-wide">TechMart</h1>
        <p class="text-2xl font-light italic">Aqui você encontra aquilo que busca.</p>
      </div>
    </div>

    <main class="flex-1 flex justify-center items-center px-4 py-10">
      <div class="w-full max-w-5xl bg-white rounded-3xl p-10 shadow space-y-10">
        <h2 class="text-2xl font-bold text-neutral-800 text-center">Nossos Produtos em destaques</h2>

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

      </div>
    </main>
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

const totalPages = computed(() => Math.ceil(products.value.length / itemsPerPage));

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