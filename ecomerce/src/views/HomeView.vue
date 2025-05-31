<template>
  <div class="min-h-screen flex flex-col bg-gray-100">
    <div class="w-full h-[400px] bg-cover bg-center bg-no-repeat"
      style="background-image: url('https://img.freepik.com/fotos-gratis/luminaria-de-neon-para-vendas-de-sexta-feira-negra_23-2151833076.jpg?semt=ais_hybrid&w=740');">
      <div class="h-full flex flex-col justify-center pl-20 text-white bg-black/60">
        <h1 class="text-6xl font-bold mb-4 tracking-wide">TechMart</h1>
        <p class="text-2xl font-light italic">Aqui você encontra aquilo que busca.</p>
      </div>
    </div>

    <main class="flex-1 flex flex-col justify-center items-center px-4 py-10 space-y-10">
      <!-- Ofertas primeiro -->
      <div class="w-full max-w-[90vw] bg-white rounded-3xl p-10 shadow">
        <ProductCardComponent title="Ofertas Imperdíveis"
          apiUrl="https://dummyjson.com/products?limit=24&skip=10&sort=price" :showDiscount="true" />
      </div>

      <!-- Produtos em destaque depois -->
      <div class="w-full max-w-[90vw] bg-white rounded-3xl p-10 shadow">
        <ProductCardComponent title="Produtos em Destaque" apiUrl="https://dummyjson.com/products?limit=24" />
      </div>
    </main>
  </div>
</template>

<script setup>
import ProductCardComponent from '../components/ProductCardComponent.vue'
</script>