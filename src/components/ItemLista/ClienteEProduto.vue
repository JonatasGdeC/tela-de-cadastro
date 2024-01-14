<script>
export default {
  props: {
    cliente: Object,
    produtos: Array,
  },

  data() {
    return {
      produtoSelecionado: '',
    }
  },

  mounted() {
    this.cliente.produtos = this.cliente.produtos || []
    if (!this.cliente.produtos.length) {
      const produtosAssociados = JSON.parse(
        localStorage.getItem(`produtos_cliente_${this.cliente.nome}`),
      )
      this.cliente.produtos = produtosAssociados || []
    }

    const produtosAssociados = JSON.parse(
      localStorage.getItem(`produtos_cliente_${this.cliente.nome}`),
    )
    if (produtosAssociados) {
      this.cliente.produtos = produtosAssociados
    }
  },

  methods: {
    adicionarProduto() {
      this.cliente.produtos = this.cliente.produtos || []

      if (this.produtoSelecionado === '') {
        alert('Selecione o produto no campo esquerdo do card...')
      }

      if (this.produtoSelecionado) {
        this.cliente.produtos.push({ nome: this.produtoSelecionado })
        this.atualizarLocalStorage()
        this.produtoSelecionado = ''
      }
    },

    excluirProduto() {
      const indexToRemove = this.cliente.produtos.findIndex(
        (produto) => produto.nome === produto.nome,
      )
      if (indexToRemove !== -1) {
        this.cliente.produtos.splice(indexToRemove, 1)
        this.atualizarLocalStorage()
      }
    },

    atualizarLocalStorage() {
      localStorage.setItem(
        `produtos_cliente_${this.cliente.nome}`,
        JSON.stringify(this.cliente.produtos),
      )
    },
  },
}
</script>

<template>
  <section class="card">
    <div class="informacoe">
      <div class="informacoe_linha">
        <p>Cliente:</p>
        <p>{{ cliente.nome }}</p>
      </div>
      <div class="informacoe_linha">
        <p>Produtos:</p>
        <select class="informacoe_linha_input" v-model="produtoSelecionado">
          <option v-for="produto in produtos" :key="produto.id">
            {{ produto.nome }}
          </option>
        </select>
      </div>
      <ul class="card_list">
        <li
          class="card_list_item"
          v-for="produto in cliente.produtos"
          :key="produto.nome"
        >
          {{ produto.nome }}
          <button
            @click="excluirProduto"
            class="card_list_item_button"
            title="Excluir produto do usuário"
          >
            X
          </button>
        </li>
      </ul>
    </div>
    <div class="acoes">
      <button @click="adicionarProduto" class="acoes_btn acoes_btn_add">
        Adicionar Produto
      </button>
    </div>
  </section>
</template>
