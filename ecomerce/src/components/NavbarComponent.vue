<template>
  <nav class="bg-[#080C1C] p-4 shadow-lg">
    <div class="container mx-auto flex justify-between items-center">
      <!-- Botão Sidebar -->
      <button @click="$emit('toggle-sidebar')"
        class="text-[#F8F8F8] hover:text-[#4FACFE] transition-colors duration-200">
        <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16M4 18h16" />
        </svg>
      </button>

      <!-- Área de Pesquisa -->
      <div class="flex-1 mx-4">
        <div class="max-w-xl mx-auto relative">

          <!-- Campo de busca -->
          <input type="text" v-model="busca" placeholder="Digite aqui..."
            class="w-full px-4 py-2 rounded-lg bg-[#080C1C] border border-[#4FACFE]/30 text-[#F8F8F8] placeholder-[#F8F8F8]/50 focus:outline-none focus:border-[#4FACFE] focus:ring-1 focus:ring-[#4FACFE]" />

          <!-- Sugestões -->
          <div v-if="busca && produtosEncontrados.length"
            class="absolute w-full mt-2 py-2 bg-[#080C1C] border border-[#4FACFE]/30 rounded-lg">
            <div v-for="produto in produtosEncontrados" :key="produto.id" @click="irParaProduto(produto)"
              class="px-4 py-2 hover:bg-[#4FACFE]/10 cursor-pointer text-[#F8F8F8]">
              {{ produto.title }}
            </div>
          </div>
        </div>
      </div>

      <!-- Logo -->
      <RouterLink to="/" class="font-bold text-xl hover:opacity-80 transition-opacity duration-200">
        <span class="brand-gradient">TechMart</span>
      </RouterLink>
    </div>
  </nav>
</template>

<script>
import axios from 'axios'

export default {
  data() {
    return {
      busca: '',
      produtos: [],
      produtosEncontrados: []
    }
  },
  watch: {
    busca() {
      this.buscarProdutos()
    }
  },
  methods: {
    async carregarProdutos() {
      try {
        const response = await axios.get('https://dummyjson.com/products?limit=300')
        this.produtos = response.data.products
      } catch (erro) {
        console.error('Erro:', erro)
      }
    },
    buscarProdutos() {
      if (!this.busca) {
        this.produtosEncontrados = []
        return
      }

      const termo = this.busca.toLowerCase()
      this.produtosEncontrados = this.produtos
        .filter(p =>
          p.title.toLowerCase().includes(termo) ||
          p.category.toLowerCase().includes(termo)
        )
        .slice(0, 5)
    },
    irParaProduto(produto) {
      this.$router.push(`/produtos/item/${produto.id}`)
      this.busca = ''
      this.produtosEncontrados = []
    }
  },
  mounted() {
    this.carregarProdutos()
  }
}
</script>

<style scoped>
.brand-gradient {
  background: linear-gradient(90deg, #4FACFE, #8CE7FE, #4FACFE, #8CE7FE);
  background-size: 200% 200%;
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  color: transparent;
  animation: gradientMove 3s linear infinite;
}

@keyframes gradientMove {
  0% {
    background-position: 0% 50%;
  }

  100% {
    background-position: 100% 50%;
  }
}
</style>
