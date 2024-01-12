<script>
import './styles.scss'

export default {
  props: ['selectedTab'],
  methods: {
    changeTab(tab) {
      this.$emit('changeTab', tab);
    }
  },
}

</script>

<template>
  <div class="header">
    <div class="header_buttons">
      <button
        :class="{ 'header_buttons_button--active': selectedTab === 'clientes' }"
        @click="changeTab('clientes')"
        class="header_buttons_button"
        title="Cadastro e Lista de Clientes">
        Clientes
      </button>
      <button
        :class="{ 'header_buttons_button--active': selectedTab === 'produtos' }"
        @click="changeTab('produtos')"
        class="header_buttons_button"
        title="Cadastro e Lista de Produtos">
        Produtos
      </button>
      <button
      :class="{ 'header_buttons_button--active': selectedTab === 'clientesEprodutos' }"
      @click="changeTab('clientesEprodutos')"
      class="header_buttons_button"
      title="Associação de cliente com produto">
        Clientes e Produtos
      </button>
    </div>
  </div>
</template>
