<script setup>
import { ref } from 'vue'
import Navbar from './components/NavbarComponent.vue'
import Sidebarcomponent from './components/Sidebarcomponent.vue'
import Footer from './components/FooterComponent.vue'

const sidebarAberta = ref(false)
const alternarSidebar = () => sidebarAberta.value = !sidebarAberta.value
const fecharSidebar = () => sidebarAberta.value = false
</script>

<template>
  <div class="min-h-screen flex flex-col relative">
    <!-- Overlay -->
    <div
      v-if="sidebarAberta"
      class="fixed inset-0 bg-black/40 z-40"
      @click="fecharSidebar"
    ></div>

    <!-- Sidebar -->
    <Sidebarcomponent v-if="sidebarAberta" class="z-50" />

    <!-- Navbar -->
    <Navbar @toggle-sidebar="alternarSidebar" />

    <main class="flex-grow">
      <RouterView />
    </main>
    <Footer />
  </div>
</template>
