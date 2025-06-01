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
          <input type="text" v-model="textoBusca" placeholder="Digite aqui..." class="w-full px-4 py-2 rounded-lg bg-[#080C1C] border border-[#4FACFE]/30 
                   text-[#F8F8F8] placeholder-[#F8F8F8]/50
                   focus:outline-none focus:border-[#4FACFE] focus:ring-1 focus:ring-[#4FACFE]" />

          <!-- Lista de sugestões -->
          <div v-if="textoBusca && produtosEncontrados.length > 0"
            class="absolute w-full mt-2 py-2 bg-[#080C1C] border border-[#4FACFE]/30 rounded-lg">
            <div v-for="produto in produtosEncontrados" :key="produto.id"
              class="px-4 py-2 hover:bg-[#4FACFE]/10 cursor-pointer text-[#F8F8F8]" @click="irParaProduto(produto)">
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

<script setup>
import { ref } from 'vue'
import { RouterLink, useRouter } from 'vue-router'

// Emits para o sidebar
defineEmits(['toggle-sidebar'])

const router = useRouter()
const textoBusca = ref('')
const listaProdutos = ref([])
const produtosEncontrados = ref([])

// Buscar produtos quando o componente carregar
async function buscarProdutos() {
    try {
      const resposta = await fetch('https://dummyjson.com/products?limit=300')
      const dados = await resposta.json()

      if (!dados.products) {
        console.error('Dados inválidos recebidos da API')
        return
      }

      listaProdutos.value = dados.products
      console.log(`Carregados ${dados.products.length} produtos`) // Debug
    } catch (erro) {
      console.error('Erro ao carregar produtos:', erro)
    }
  }

// Procurar produtos quando digitar
function procurarProdutos() {
    if (!textoBusca.value) {
      produtosEncontrados.value = []
      return
    }

    const busca = textoBusca.value.toLowerCase()
    produtosEncontrados.value = listaProdutos.value
      .filter(produto =>
        produto.title.toLowerCase().includes(busca) ||
        produto.description.toLowerCase().includes(busca) ||
        produto.category.toLowerCase().includes(busca)
      )
      .slice(0, 5) //altera o numero de sugestões 
  }

// Vai para a pagina do produto 
function irParaProduto(produto) {
    router.push(`/produtos/item/${produto.id}`)
    textoBusca.value = ''
    produtosEncontrados.value = []
  }

// analisa a mudança do texto ( Quando vai adicionando as letras )
import { watch } from 'vue'
watch(textoBusca, () => {
  procurarProdutos()
})

// Carregar produtos quando iniciar
import { onMounted } from 'vue'
onMounted(() => {
  buscarProdutos()
})
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
  0% { background-position: 0% 50%; }
  100% { background-position: 100% 50%; }
}
</style>
