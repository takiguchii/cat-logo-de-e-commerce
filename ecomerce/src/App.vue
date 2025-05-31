<script setup>
import { ref } from 'vue'
import { RouterView } from 'vue-router'
import Navbar from './components/NavbarComponent.vue'
import Footer from './components/FooterComponent.vue'
import Sidebarcomponent from './components/Sidebarcomponent.vue'

const sidebarAberta = ref(false)

function alternarSidebar() {
  sidebarAberta.value = !sidebarAberta.value
}
</script>

<template>
  <div class="min-h-screen flex flex-col relative">
    <!-- Sidebar -->
    <Sidebarcomponent v-if="sidebarAberta" />

    <!-- Navbar com botão que emite toggle -->
    <Navbar @toggle-sidebar="alternarSidebar" />

    <!-- Conteúdo principal -->
    <main class="flex-grow">
      <RouterView />
    </main>

    <Footer />
  </div>
</template>
