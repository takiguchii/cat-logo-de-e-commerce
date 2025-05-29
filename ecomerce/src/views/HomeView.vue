<template>
  <div class="min-h-screen flex flex-col bg-gray-100">
    <!-- Parte superior com imagem de fundo -->
    <div
      class="w-full h-[400px] bg-cover bg-center bg-no-repeat"
      style="background-image: url('https://via.placeholder.com/1200x400');"
    >
      <!-- Conteúdo sobre a imagem, se quiser -->
      <div class="h-full flex items-center justify-center text-white text-3xl font-bold bg-black/60">
        Imagem de fundo do site
      </div>
    </div>

    <!-- Conteúdo abaixo -->
    <main class="flex-1 flex justify-center items-center">
      <div class="w-full max-w-3xl bg-white rounded-3xl p-10 shadow">
        Conteúdo da página
      </div>
    </main>
  </div>
</template>

