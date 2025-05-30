<template>
  <div class="min-h-screen flex flex-col bg-gray-100">
    <!-- espaçamento  -->
    <div
      class="w-full h-[400px] bg-cover bg-center bg-no-repeat"
      style="background-image: url('https://img.freepik.com/fotos-gratis/luminaria-de-neon-para-vendas-de-sexta-feira-negra_23-2151833076.jpg?semt=ais_hybrid&w=740');"
    >
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
        <div class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-5 gap-6">
          <!-- CARDS -->
          <div class="bg-gray-100 p-6 rounded-2xl shadow hover:shadow-2xl transition duration-300">
            <h3 class="text-lg font-semibold text-neutral-800 text-center">Categoria 1</h3>
            <p class="text-sm text-neutral-600 mt-2">Descrição breve da categoria.</p>
          </div>
          <div class="bg-gray-100 p-6 rounded-2xl shadow hover:shadow-2xl transition duration-300">
            <h3 class="text-lg font-semibold text-neutral-800 text-center">Categoria 2</h3>
            <p class="text-sm text-neutral-600 mt-2">Descrição breve da categoria.</p>
          </div>
          <div class="bg-gray-100 p-6 rounded-2xl shadow hover:shadow-2xl transition duration-300">
            <h3 class="text-lg font-semibold text-neutral-800 text-center">Categoria 3</h3>
            <p class="text-sm text-neutral-600 mt-2">Descrição breve da categoria.</p>
          </div>
          <div class="bg-gray-100 p-6 rounded-2xl shadow hover:shadow-2xl transition duration-300">
            <h3 class="text-lg font-semibold text-neutral-800 text-center">Categoria 4</h3>
            <p class="text-sm text-neutral-600 mt-2">Descrição breve da categoria.</p>
          </div>
          <div class="bg-gray-100 p-6 rounded-2xl shadow hover:shadow-2xl transition duration-300">
            <h3 class="text-lg font-semibold text-neutral-800 text-center">Categoria 5</h3>
            <p class="text-sm text-neutral-600 mt-2">Descrição breve da categoria.</p>
          </div>
        </div>
          <div class="flex justify-center mt-6">
            <button class="bg-neutral-800 text-white px-6 py-3 rounded-full hover:bg-blue-700/90 transition duration-300">
              Ver mais categorias
            </button>
          </div>
      </div>
    </main>
  </div>
</template>

