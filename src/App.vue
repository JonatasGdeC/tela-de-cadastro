<script>
import Menu from './containers/Menu.vue'
import Clientes from './containers/Clientes.vue'
import Produtos from './containers/Produtos.vue'
import ClientesEProdutos from './containers/ClientesEProdutos.vue'

export default {
  data() {
    return {
      selectedTab: 'clientesEprodutos',
    }
  },
  methods: {
    changeTab(tab) {
      this.selectedTab = tab
    },
  },
  components: {
    Menu,
    Clientes,
    Produtos,
    ClientesEProdutos,
  },
}
</script>

<template>
  <Menu :selectedTab="selectedTab" @changeTab="changeTab" />
  <div class="container">
    <ClientesEProdutos v-if="selectedTab === 'clientesEprodutos'" />
    <Clientes v-else-if="selectedTab === 'clientes'" />
    <Produtos v-else-if="selectedTab === 'produtos'" />
  </div>
</template>
