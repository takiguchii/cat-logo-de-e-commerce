<template>
  <div class="min-h-screen flex flex-col bg-gray-100">
    <!-- espaçamento  -->
    <div class="w-full h-[400px] bg-cover bg-center bg-no-repeat"
      style="background-image: url('https://img.freepik.com/fotos-gratis/luminaria-de-neon-para-vendas-de-sexta-feira-negra_23-2151833076.jpg?semt=ais_hybrid&w=740');">
      <!-- Frase em cima da imaghem de fundo  -->
      <div class="h-full flex flex-col justify-center pl-20 text-white bg-black/60">
        <h1 class="text-6xl font-bold mb-4 tracking-wide">TechMart</h1>
        <p class="text-2xl font-light italic">Aqui você encontra aquilo que busca.</p>
      </div>
    </div>

    <!-- Conteudo do ecomerce  -->
    <main class="flex-1 flex justify-center items-center px-4 py-10">
      <div class="w-full max-w-3xl bg-white rounded-3xl p-10 shadow space-y-10">
        <h2 class="text-2xl font-bold text-neutral-800 text-center">Categorias</h2>
        <div v-if="loading" class="text-center">
          <p class="text-gray-600">Carregando categorias...</p>
        </div>
        <div v-else class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-5 gap-6">
          <CategoryCard v-for="category in categories" :key="category" :category-name="category" />
        </div>
      </div>
    </main>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import CategoryCard from '@/components/CategoryCard.vue';

const loading = ref(true);
const categories = ref([]);

const fetchCategories = async () => {
  try {
    const response = await fetch('https://dummyjson.com/products/categories');
    const data = await response.json();
    categories.value = data.slice(0, 5);
    loading.value = false;
  } catch (error) {
    console.error('Error fetching categories:', error);
    loading.value = false;
  }
};

onMounted(() => {
  fetchCategories();
});
</script>
