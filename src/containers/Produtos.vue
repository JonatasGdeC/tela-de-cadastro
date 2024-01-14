<script>
import './styles.scss'
import FormProduto from '../components/FormCadastro/Produto.vue'
import ItemListaProdutos from '../components/ItemLista/Produto.vue'

export default {
  emits: ['cadastrar'],

  data() {
    return {
      mostrarFormulario: false,
      mensagemBTN: 'Cadastrar',
      produtos: [],
      produtosInativos: [],
    }
  },

  mounted() {
    this.carregarDadosDoLocalStorage()
  },

  beforeUnmount() {
    this.salvarDadosNoLocalStorage()
  },

  methods: {
    carregarDadosDoLocalStorage() {
      const storedProdutos = localStorage.getItem('produtos')
      const storedProdutosInativos = localStorage.getItem('produtosInativos')

      if (storedProdutos) {
        this.produtos = JSON.parse(storedProdutos)
      }

      if (storedProdutosInativos) {
        this.produtosInativos = JSON.parse(storedProdutosInativos)
      }
    },

    salvarDadosNoLocalStorage() {
      const jsonStringProdutos = JSON.stringify(this.produtos)
      const jsonStringProdutosInativos = JSON.stringify(this.produtosInativos)

      localStorage.setItem('produtos', jsonStringProdutos)
      localStorage.setItem('produtosInativos', jsonStringProdutosInativos)
    },

    btnPrincipal() {
      if (this.mostrarFormulario === false) {
        this.mostrarFormulario = true
        this.mensagemBTN = 'Cancelar'
      } else {
        this.mostrarFormulario = false
        this.mensagemBTN = 'Cadastrar'
      }
    },

    cadastrarProduto(produto) {
      produto.ativo = true
      this.produtos.push(produto)
      this.mostrarFormulario = false
      this.mensagemBTN = 'Cadastrar'

      const jsonString = JSON.stringify(this.produtos)
      localStorage.setItem('produtos', jsonString)
    },

    alterarEstadoProduto(produto) {
      produto.ativo = !produto.ativo
      if (!produto.ativo) {
        const index = this.produtos.indexOf(produto)
        if (index !== -1) {
          this.produtos.splice(index, 1)
          this.produtosInativos.push(produto)
        }
      } else {
        const index = this.produtosInativos.indexOf(produto)
        if (index !== -1) {
          this.produtosInativos.splice(index, 1)
          this.produtos.push(produto)
        }
      }
      const jsonString = JSON.stringify(this.produtos)
      localStorage.setItem('produtos', jsonString)
    },

    excluirProdutoDoLocalStorage(produto) {
      const confirmacao = window.confirm(
        'Deseja realmente excluir este produto?',
      )

      if (confirmacao) {
        const index = this.produtos.indexOf(produto)
        if (this.produtos.includes(produto)) {
          this.produtos.splice(index, 1)
          const jsonString = JSON.stringify(this.produtos)
          localStorage.setItem('produtos', jsonString)
        } else {
          this.produtosInativos.splice(index, 1)
          const jsonString = JSON.stringify(this.produtosInativos)
          localStorage.setItem('produtosInativos', jsonString)
        }
      }
    },
  },
  components: {
    FormProduto,
    ItemListaProdutos,
  },
}
</script>

<template>
  <button
    @click="btnPrincipal"
    class="btn-cadastrar"
    :class="{ 'btn-cadastrar--cancelar': mensagemBTN === 'Cancelar' }"
  >
    {{ mensagemBTN }}
  </button>
  <FormProduto v-if="mostrarFormulario" @cadastrar="cadastrarProduto" />

  <div v-if="produtos.length > 0 || produtosInativos.length > 0">
    <ul class="list">
      <li class="list_item">
        <ItemListaProdutos
          v-for="(produto, index) in produtos"
          :key="index"
          :produto="produto"
          @excluir-produto="excluirProdutoDoLocalStorage"
          @alterar-estado="alterarEstadoProduto"
        />
      </li>
    </ul>

    <div class="list_inativos" v-if="produtosInativos.length > 0">
      <h3 class="list_title">Produtos Desativados</h3>
      <ul class="list--inativos_card">
        <li class="list_item">
          <ItemListaProdutos
            v-for="(produto, index) in produtosInativos"
            :key="index"
            :produto="produto"
            @excluir-produto="excluirProdutoDoLocalStorage"
            @alterar-estado="alterarEstadoProduto"
          />
        </li>
      </ul>
    </div>
  </div>
  <div v-else class="list_inexistente">
    <h2>Não há produtos cadastrados</h2>
  </div>
</template>
