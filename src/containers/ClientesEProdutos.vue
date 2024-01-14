<script>
import './styles.scss'
import ItemListaClienteEProduto from '../components/ItemLista/ClienteEProduto.vue'

export default {
  components: {
    ItemListaClienteEProduto,
  },
  data() {
    return {
      clientes: [],
      produtos: [],
    }
  },
  mounted() {
    this.clientes = JSON.parse(localStorage.getItem('clientes'))
    this.produtos = JSON.parse(localStorage.getItem('produtos'))
  },
}
</script>

<template>
  <div class="list_inexistente" v-if="clientes.length === 0">
    <h2>Não há clientes ativos</h2>
  </div>
  <div class="list_inexistente" v-else-if="produtos.length === 0">
    <h2>Não há produtos ativos</h2>
  </div>
  <div v-else>
    <ul class="list">
      <li class="list_item">
        <ItemListaClienteEProduto
          v-for="cliente in clientes"
          :key="cliente.nome"
          :cliente="cliente"
          :produtos="produtos"
        />
      </li>
    </ul>
  </div>
</template>
